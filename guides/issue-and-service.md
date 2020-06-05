---
description: >-
  Issue a simple loan on the deployed ACTUS Protocol contracts and progess its
  state
---

# Issue and service a Loan

## Scenario

This guide covers a simple workflow for off-chain order creation and on-chain issuance & settlement. The creator forges "orders" that represent offers to go into contractual relationship with a counterparty under specified terms. These orders could be used to create a simple OTC market.

In the scenario we have a creator, which is the lender and a counterparty which takes the role of the debtor. An order for a loan of 1000 DAI at 5% annual interest is created. The debtor countersigns the order and submits it to the blockchain.

In this guide you will:

* Choose a template and define the terms of the asset
* Create and sign an order for the asset
* Co-sign the order as the counterparty and issue the asset through ACTUS Protocol
* Service the asset by paying the principal of the loan to the debtor \(counterparty\)

## Configure the template and create an order

We assume you have completed the [Getting started](getting-started.md) guide. 

First, set yourself as the creator, optionally set the address for the counterparty \(the party that will take out the loan\) if you know it in advance and choose a template from the available templates.

To speed up things up, we go with an already registered template which defines a simple loan. \(You can find all the currently registered templates in the [repository](https://github.com/atpar/ap-monorepo/tree/master/packages/ap-contracts/templates/goerli).\)

```typescript
import { AP, Order } from '@atpar/ap.js';

// -------------------------------------------------------------
// refer to the "Getting started" section for initializing ap.js
// -------------------------------------------------------------

const creator = (await web3.eth.getAccounts())[0];
const counterparty; // address of counterparty

// choose a registered template which defines a simple PAM-based
// loan with monthly interest payments from the TemplateRegistry
const templateId = '0xf897c17a13a2ad8da2f3462857d4616f23200739c855de2de84df8950b8e28c4'; 
```

Next, parameterize the template to your wishes by setting its terms. The `CustomTerms` object is documented [here](https://ap-js.actus-protocol.io/interfaces/customterms.html). To understand the meaning of the terms parameters, you can have a look at the [ACTUS Dictionary](https://github.com/actusfrf/actus-dictionary/blob/master/actus-dictionary-terms.json). These terms need to be negotiated with the counterparty.

```typescript
// parameterize the template

// We will deribve the customTerms from the default terms of our template
const customTerms = ap.utils.conversion.deriveCustomTerms(terms);

// It is also possible to use your own set of custom terms and derive the object like s
// const customTerms = ap.utils.conversion.deriveCustomTermsFromTermsAndTemplateTerms(updatedTerms, templateTerms);

```

Now a set of order parameter is created.[ Consult the documentation](https://ap-js.actus-protocol.io/interfaces/orderparams.html%20) for a description of all possible parameters.

```typescript
// orderParams object for an asset without enhancements
const orderParams = {
  termsHash: ap.utils.constants.ZERO_BYTES32, // optional store a hash of all terms attributes
  templateId,
  customTerms,
  ownership: {
    creatorObligor: creator, // has to fulfill all obligations for the creator side
    creatorBeneficiary: creator, // receives all positive cash flow of the creator side
    counterpartyObligor: counterparty, // has to fulfill all obligations for the counterparty
    counterpartyBeneficiary: counterparty // receives all positive cash flow for the counterparty
  },
  expirationDate: String(customTerms.anchorDate), // after this date the order cannot be submitted on chain
  engine: ap.contracts.pamEngine.options.address, // address of the ACTUS PAM engine
  admin: ap.utils.constants.ZERO_ADDRESS // optional set a admin address for the ability to modify the asset once issued
} 
```

Once the terms and order parameters have been set, we can create the actual order and sign it with our Ethereum account. 

```typescript
// create the order
const order = Order.create(ap, orderParams);

// sign the order as the creator
await order.signOrder();

// obtain the order in a serialized format to be send to 
// the counterparty or a relayer service
const orderData = order.serializeOrder();
```

This is the point where we hand over to the counterparty, who wants to take out the loan.

## Take the order as the counterparty and issue the asset

When the counterparty has received the order, she instantiates the order, signs it and issues it on Ethereum. She could also send the signed OrderData object to a third party relayer for issuance.

```typescript
// -------------------------------------------------------------
// continue as counterparty
// -------------------------------------------------------------

const counterparty = (await web3.eth.getAccounts())[1];
const orderData; // obtain orderData through a communication channel

// instantiate an order through orderData
const order = Order.load(orderData);

// sign the order as counterparty
await order.signOrder();

// issue the filled order on Ethereum
await order.issueAssetFromOrder();

// -------------------------------------------------------------
// retrieve the issued asset
// -------------------------------------------------------------

ap.onNewAssetIssued(async (asset) => {
  console.log(await asset.getTerms());
});
```

## Maintaining the asset

Now the lender has to pay the principal of the loan to the debtor. The lender has to set sufficient allowance for the `AssetActor`, such that the Actor contract can transfer the principal amount to the borrower on the lenders behalf. If the `AssetActor` is not able to transfer the principal \(e.g. due to insufficient allowance or insufficient funds\) the Actor contract will transition the asset to non-performing \(risking additional penalty payments or contract default\). 

```typescript
// -------------------------------------------------------------
// settle the initial exchange as the lender (creator)
// -------------------------------------------------------------

// obtain the next obligation
const { eventType, scheduleTime } = ap.utils.schedule.decodeEvent(
  await asset.getNextScheduledEvent()
);

// assume scheduleTime >= Math.round((new Date()).getTime() / 1000);
// pre-payments are currently not supported

const { amount, token } = await asset.getNextScheduledPayment();

// set the allowance for the Actor to settle the obligation
// on behalf of the creator
await asset.approveNextScheduledPayment();

// settle the initial exchange and progress the state of the asset.
// This actually transfers the required ammount of tokens.
await asset.progress();
```

The entire projected schedule of the asset can be evaluated via:

```typescript
const schedule = await asset.getSchedule();
let state = await ap.contracts.pamEngine.methods.computeInitialState(terms);

for (event of schedule) {
  const payoff = ap.contracts.pamEngine.methods.computePayoffForEvent(
    terms,
    state,
    event,
    ap.utils.constants.ZERO_BYTES32
  );
  const state = ap.contracts.pamEngine.methods.computeStateForEvent(
    terms,
    state,
    event,
    ap.utils.constants.ZERO_BYTES32
  );
  
  console.log('Event: ' + ap.utils.schedule.decodeEvent(event));
  console.log('Events payoff: ' + payoff);
  console.log('State: ' + state);
  console.log();
}
```



