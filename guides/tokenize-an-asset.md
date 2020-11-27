---
description: Tokenize the cash flow as a beneficiary of an asset
---

# Tokenize an asset

## Scenario

When an asset is issued its not automatically also "tokenized". In ACTUS Protocol, tokenization means to create a token that represents a certain type of cash flow of the asset. In the most simple case the beneficiary, e.g. the creditor, issues a number of tokens that represent a fraction of all positive cash flow, i.e. the interest and principal payments of the asset.

In this guide the creator and beneficiary of the asset creates an ERC-20 token extended with the Funds Distribution Standard \(ERC-2222\). As a token holder she withdraws her portion of the cash flow.

In this guide you will:

* Load an existing asset
* Tokenize an asset
* Withdraw your fraction of the cash flow from the token contract

## Initialize the Funds Distribution Token

Begin with instantiating an existing ACTUS asset for which you are the beneficiary. The asset is identified by its _asset id_ that was returned during creation. Use this asset id to derive the settlement token \(currency\) address from the asset terms.

As a beneficiary, you have the right to tokenize your side of the contract. Make sure to set sensible parameters as this is how the token will be represented in many wallets. Also be sure to understand the effects of the initial supply parameter. In order to avoid rounding errors and the likes, it makes sense to multiply it with 10^18 \(`web3.utils.toWei()`\).

```typescript
import { AP } from '@atpar/protocol';
import VanillaFDTArtifact from '@atpar/protocol/build/contracts/contracts/Extensions/FDT/VanillaFDT/VanillaFDT.sol/VanillaFDT.json';

// -------------------------------------------------------------
// refer to the "Getting started" section for initializing ap.js
// -------------------------------------------------------------

const creatorBeneficiary = (await web3.eth.getAccounts())[0];
const fractionalOwner = (await web3.eth.getAccounts())[1];

// derive terms and currency address with ASSET_ID 
const terms = await ap.contracts.pamRegistry.methods.getTerms(ASSET_ID).call();
const settlementTokenAddress = terms.currency;

// set initialization arguments and the deploy the FDT
const name = 'FundsDistributionToken';
const symbol = 'FDT';
const initialAmount = web3.utils.toWei('100'); // minted to owner

const fdtContract = (new web3.eth.Contract(VanillaFDTArtifact.abi)).deploy({ 
    data: VanillaFDTArtifact.bytecode, 
    [name, symbol, settlementTokenAddress, creatorBeneficiary, initialAmount]
}).send({ from: creatorBeneficiary });

// send 20 tokens so that fractionalOwner now owns 20/100 of the created tokens
// and thus owns the rights to a 1/5 share of incoming payments 
await fdtContract.methods.transfer(
    fractionalOwner,
    web3.utils.toWei('20')
).send({ from: creatorBeneficiary });
```

### Tokenize the asset

Now that we have created the FDT as a vehicle for fractional ownership of settlement token payments, we must set the FDT contract as the beneficiary of incoming payments made on an asset. To do this we need to call the appropriate asset registry contract to update the creator beneficiary.

```typescript
await ap.contracts.pamRegistry.methods.setCreatorBeneficiary(
    ASSET_ID,
    fdt.options.address
).send({from: creatorBeneficiary});
```

### Withdraw Funds

Later, when some payments by the debtor have been made, the token holders can withdraw their portion at any time. She can also sell/send/give away tokens to other people. The ERC-20 token, extended with the ERC-2222 standard automatically takes care of the accounting.

```typescript
// -------------------------------------------------------------
// withdrawing funds paid into the FDT
// -------------------------------------------------------------

// the internal balances of the FDT have to be update
await fdt.methods.updateFundsReceived().send({from: anyone})

// retrieve the current accrued amount of a holder
await fdt.methods.withdrawableFundsOf(fractionalOwner).call();

// withdrawing the accrued amount for a holder
await fdt.methods.withdrawFunds().send({ from: fractionalOwner });
```

