# Issue and service a Loan

Content

* Assumes getting started
* Creditor: Alice, Debtor: Bob
* Choose parameters
* Prepare tx object
* Issue Loan
* Service Loan \(Alice & Bob\)

```typescript
import { AP, Order } from './ap.js';

// -------------------------------------------------------------
// refer to the "Getting started" section for initializing ap.js
// -------------------------------------------------------------

const creator = (await web3.eth.getAccounts())[0];
const counterparty; // address of counterparty

// choosing a registered product which defines a simple PAM 
// based loan with monthly interest payments from the ProductRegistry
const productId = '...';

// parameterize the product
const customTerms = {
  anchorDate: Math.round((new Date()).getTime() / 1000);,
  notionalPrincipal: ap.utils.toPrecision(1000), // e.g. 1000 DAI
  nominalInterestRate: ap.utils.toPrecision(0.05), // e.g. 5%
  premiumDiscountAtIED: '0',
  rateSpread: '0',
  lifecap: '0',
  lifeFloor: '0',
  coverageOfCreditEnhancement: '0',
  contractReference_1: {
    object: ap.utils.constants.ZERO_BYTES32,
    contractReferenceType: '0',
    contractReferenceRole: '0'
  },
  contractReference_2: {
    object: ap.utils.constants.ZERO_BYTES32,
    contractReferenceType: '0',
    contractReferenceRole: '0'
  }
};
 
// orderParams object for an asset without enhancements
const orderParams = {
  termsHash: ap.utils.constants.ZERO_BYTES32, // optional store a hash of all terms attributes
  productId,
  customTerms,
  ownership: {
    creatorObligor: creator, // has to all fulfill obligations for the creator side
    creatorBeneficiary: creator, // receives all revenue of the creator
    counterpartyObligor: counterparty, // has to all fulfill obligations for the counterparty
    counterpartyBeneficiary: counterparty // receives all revenue of the counterparty
  },
  expirationDate: String(customTerms.anchorDate),
  engine: ap.contracts.pamEngine.options.address // address of the PAM engine
} 

// creating the order
const order = Order.create(ap, orderParams);

// signing the order as the creator
await order.signOrder();

// obtaining the order in a serialized format to be send to a relayer service
const orderData = order.serializeOrder();

// -------------------------------------------------------------
// continuing as counterparty ...
// -------------------------------------------------------------

const counterparty = (await web3.eth.getAccounts())[0];
const orderData; // obtain orderData through a communication channel

// instantiating an order through orderData
const order = Order.load(orderData);

// signing the order as counterparty
await order.signOrder();

// issuing the filled order
await order.issueAssetFromOrder();

// -------------------------------------------------------------
// retrieving the issued asset
// -------------------------------------------------------------

ap.onNewAssetIssued(async (asset) => {
  console.log(await asset.getTerms());
});
```

```typescript
// -------------------------------------------------------------
// settling the initial exchange as the lender (creator)
// -------------------------------------------------------------

// obtaining the next obligation
const { eventType, scheduleTime } = ap.utils.schedule.decodeEvent(
  asset.getNextEvent()
);

// assuming scheduleTime >= Math.round((new Date()).getTime() / 1000);
// pre-payments are currently not supported

const { amount, token } = await asset.getNextPayment();

// setting allowance for the Actor to settle the obligation
// on behalf of the creator
await IERC20(token).methods.approve(
  ap.contracts.assetActor.options.address,
  amount
);

// settle the initial exchange and progress the state of the asset
await asset.progress();
```



