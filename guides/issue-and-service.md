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

* Define the terms of the asset
* Issue the asset through ACTUS Protocol
* Service the asset by paying the principal of the loan to the debtor \(counterparty\)

## Define the Terms

We assume you have completed the [Getting started](getting-started.md) guide. 

First, set yourself as the creator, optionally set the address for the counterparty \(the party that will take out the loan\) if you know it in advance and choose a template from the available templates.

To speed up things up, you can use the PAM terms from our[ example repository.](https://github.com/atpar/ap-js-example/blob/master/PAMTerms.json)

```typescript
import { AP } from '@atpar/protocol';

// -------------------------------------------------------------
// refer to the "Getting started" section for initializing ap.js
// -------------------------------------------------------------

const creator = (await web3.eth.getAccounts())[0];
const counterparty; // address of counterparty
const anyone = (await web3.eth.getAccounts())[2] // used to make calls that could be made by any address

// Terms for a simple PAM-based loan with monthly interest payments
const PAMTerms = require('./terms.json'); 
const terms = {
    ...PAMTerms,
    currency: '0xEcFcaB0A285d3380E488A39B4BB21e777f8A4EaC' // address of ERC20 token to use as settlement currency
}
```

Set up the asset initialization parameters:

```typescript
// set up ownership structure
const ownership = {
    creatorObligor: creator, // has to fulfill all obligations for the creator side
    creatorBeneficiary: creator, // receives all positive cash flow of the creator side
    counterpartyObligor: counterparty, // has to fulfill all obligations for the counterparty
    counterpartyBeneficiary: counterparty, // receives all positive cash flow for the counterparty
}

// Use the conversion utils method to get the schedule
const schedule = await ap.utils.schedule.computeScheduleFromTerms(ap.contracts.pamEngine, terms);

```

Use the appropriate Asset Actor contract \(in our case the PAMActor\) to initialize and register the new asset on chain:

```typescript
const initializeAssetTx = await ap.contracts.pamActor.methods.initialize(
    terms, // Asset Terms
    schedule, // Schedule generated from engine
    ownership, // Ownership structure
    ap.contracts.pamEngine.options.address, // Asset engine contract addres
    ap.utils.constants.ZERO_ADDRESS // admin address (optional)
).send({from: creator})
```

## Maintaining the asset

Now the lender has to pay the principal of the loan to the debtor. The lender has to set sufficient allowance for the `AssetActor`, such that the Actor contract can transfer the principal amount to the borrower on the lenders behalf. If the `AssetActor` is not able to transfer the principal \(e.g. due to insufficient allowance or insufficient funds\) the Actor contract will transition the asset to non-performing \(risking additional penalty payments or contract default\). 

```typescript
// -------------------------------------------------------------
// settle the initial exchange as the lender (creator)
// -------------------------------------------------------------

// obtain the next obligation
const nextScheduledEvent = await ap.contracts.pamRegistry.methods.getNextScheduledEvent(assetId).call();

const { eventType, scheduleTime } = ap.utils.schedule.decodeEvent(nextScheduledEvent);

// assume scheduleTime >= Math.round((new Date()).getTime() / 1000);
// pre-payments are currently not supported

// Approve actor to pay settlement
const amount = terms.notionalPrincipal;
const currency = terms.currency;
await ap.contracts.erc20(currency).methods.approve(
    ap.contracts.pamActor.options.address, 
    amount
);

// progress the asset
await ap.contracts.pamActor.methods.progress(assetId).send({from: anyone});
```





