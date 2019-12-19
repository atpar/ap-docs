# Tokenization

> Tokenization in ACTUS Protocol means that for a side of an ACTUS contract ownership in cash flows is represented through ownership of an Ethereum ERC-20 compatible token. 
>
> Token holders receive a percentage of the cash flow, proportional to the fraction of the token supply they own. They can withdraw their balances at any time.

Tokenization is optional. It usually makes most sense for the _Beneficiary_ side of an asset \(the side that will receive the principal and/or interest payments after the initial exchange, i.e. the loan amount, was paid\). 

ACTUS Protocol makes use of an implementation of [ERC-2222](https://github.com/ethereum/EIPs/issues/2222) to efficiently distribute cash flows to token holders.

**ADD:** 

* **Depositing**
* **Withdrawing**
* **Transferring**

{% hint style="info" %}
ACTUS Protocol currently only supports tokenization of the beneficary side of an asset
{% endhint %}

### Example

Alice lends 100 DAI to Bob. Bob pays the DAI back over the course of 1 year. Each month he pays a percentage of the principal + interest.[Tokenization](https://app.gitbook.com/@atpar/s/actus-protocol/~/drafts/-LwStONQ1lqX8usJr5QL/ap-js/tokenization/~/settings/customization)

Alice is the beneficiary and tokenizes her side of the asset. She has multiple options:

* She tokenizes all cash flow types of the asset together. For instance, she decides to issue 100 tokens. Each individual token represents exactly 1% of the future cash flow of the asset \(principal payments + interest payments\).
* She tokenizes interest payments and principal payments separately. 100 Principal Tokens and 100 Interest Tokens are created, each representing 1% of the respective cash flow type.

Let's assume the latter case. Now Alice can sell the principal & interest tokens indiviually on an ERC20 compatible market. Potential buyers can look at the underlying asset and price the tokens according to the outstanding cash flow and their individual risk assessment.

### Workflow

* Issue an AP Asset
* Use `asset.tokenizeBeneficiary()` to tokenize the beneficiary side

```typescript
const distributorAddress = await asset.tokenizeBeneficiary();
```

By default all cash-flows are included when an asset is tokenized. In order to tokenize individual cash-flows, please look at the [`TokenizationFactory()`](https://github.com/atpar/ap-monorepo/blob/MS1/packages/ap-contracts/contracts/Tokenization/TokenizationFactory.sol) in _ap-contracts_.

For more information please refer to [`tokenizeBeneficiary()`](https://ap-js.actus-protocol.io/classes/asset.html#tokenizebeneficiary) in the _AP.js_ documentation.



