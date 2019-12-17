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
  anchorDate: new Date.now(),
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
  engine: ap.contracts.pamEngine.options.address, // address of the PAM engine
  enhancement_1: null,
  enhancement_2: null
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
await order.issueFromOrder();
```





