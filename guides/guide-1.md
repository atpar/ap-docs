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

// ...

// orderParams object for an asset without enhancements
const orderParams = {
  termsHash: ap.utils.erc712.getTermsHash(terms),
  productId: productId,
  customTerms: ap.utils.convert.toCustomTerms(terms),
  ownership: {
    creatorObligor: creator, // account which has to all fulfill obligations for the creator side
    creatorBeneficiary: creator, // account which receives all revenue of the creator
    counterpartyObligor: counterparty,
    counterpartyBeneficiary: counterparty
  },
  expirationDate: String(terms.contractDealDate),
  engine: ap.contracts.pamEngine.options.address,
  enhancement_1: {
    termsHash: ap.utils.constants.ZERO_BYTES32,
    productId: ap.utils.constants.ZERO_BYTES32,
    customTerms: ap.utils.convert.toCustomTerms(terms), // arbitrary customTerms
    ownership: {
      creatorObligor: ap.utils.constants.ZERO_ADDRESS,
      creatorBeneficiary: ap.utils.constants.ZERO_ADDRESS,
      counterpartyObligor: ap.utils.constants.ZERO_ADDRESS,
      counterpartyBeneficiary: ap.utils.constants.ZERO_ADDRESS
    },
    engine: ap.utils.constants.ZERO_ADDRESS
  },
  enhancement_2: {
    termsHash: ap.utils.constants.ZERO_BYTES32,
    productId: ap.utils.constants.ZERO_BYTES32,
    customTerms: ap.utils.convert.toCustomTerms(terms), // arbitrary customTerms
    ownership: {
      creatorObligor: ap.utils.constants.ZERO_ADDRESS,
      creatorBeneficiary: ap.utils.constants.ZERO_ADDRESS,
      counterpartyObligor: ap.utils.constants.ZERO_ADDRESS,
      counterpartyBeneficiary: ap.utils.constants.ZERO_ADDRESS
    },
    engine: ap.utils.constants.ZERO_ADDRESS
  }
} 

const order = Order.create(ap, orderParams);
```

