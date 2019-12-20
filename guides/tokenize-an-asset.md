---
description: Tokenize the cash flow as a beneficiary of an asset
---

# Tokenize an asset

## Scenario

When an asset is issued it's not autmatically also "tokenized". In ACTUS Protocol, tokenization means to create a token that represents a certain type of cash flow of the asset. In the most simple case the beneficiary, e.g. the creditor, issues a number of tokens that represent a fraction of all positive cash flow, i.e. the interest and principal payments of the asset.

In this guide the creator and beneficiary of the asset creates an ERC-20 token extended with the Funds Distribution Standard \(ERC-2222\). As a token holder she withdraws her portion of the cash flow.

In this guide you will:

* Load an existing asset
* Tokenize an asset
* Withdraw your fraction of the cash flow from the token contract

## Load an asset

Begin with instantiating an existing ACTUS asset for which you are the beneficiary. The asset is identified by its _asset id_ that was returned during creation.

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


```

### Tokenize the asset 

As a beneficiary, you have the right to tokenize your side of the contract. Make sure to set sensible parameters as this is how the token will be represented in many wallets. Also be sure to understand the effects of the initial supply parameter. In order to avoid rounding errors and the likes, it makes sense to multiply it with 10^18 \(`web3.utils.toWei()`\).

```typescript
// tokenizing payments paid towards the creator beneficiary
// deploys a new FundsDistributionToken and updates the address
// of the creator beneficiary to the address of the FDT
const distributorAddress = await asset.tokenizeBeneficiary(
  web3.utils.toHex('Distributor'), // name
  web3.utils.toHex('FDT'), // symbol
  web3.utils.toWei('1000000') // initial supply
);

// (await asset.getOwnership()).creatorBeneficiary === distributorAddress;
```

### Withdraw Funds

Later, when some payments by the debtor have been made, the token holders can withdraw their portion at any time. She can also sell/send/give away tokens to other people. The ERC-20 token, extended with the ERC-2222 standard automatically takes care of the accounting.

```typescript
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

