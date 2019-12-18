# Tokenize an asset

Content

* Assume asset is issued
* Choose and set token parameters
* tokenizeBeneficiary\(\)
* transfer some of the tokens\(\)
* withdraw

```typescript
import { AP, Asset } from 'ap.js';

// -------------------------------------------------------------
// refer to the "Getting started" section for initializing ap.js
// -------------------------------------------------------------

const creatorBeneficiary = (await web3.eth.getAccounts())[0];

// loading an asset as the creator beneficiary
const asset = await Asset.load(ap, ASSET_ID);

// assuming:
// (await asset.getOwnership()).creatorBeneficiary === creatorBeneficiary;

// tokenizing payments paid towards the creator beneficiary
// deploys a new FundsDistributionToken and updates the address
// of the creator beneficiary to the address of the FDT
const distributorAddress = await asset.tokenizeBeneficiary(
  web3.utils.toHex('Distributor'),
  web3.utils.toHex('FDT'),
  web3.utils.toWei('10000')
);

// (await asset.getOwnership()).creatorBeneficiary === distributorAddress;

// -------------------------------------------------------------
// withdrawing funds paid into the FDT
// -------------------------------------------------------------

// ...
await ap.contracts.distributor(
  distributorAddress
).methods.withdrawableFundsOf(creatorBeneficiary).call();

// withdrawing ...
await ap.contracts.distributor(
  distributorAddress
).methods.withdrawFunds().send({ from: creatorBeneficiary });
```

