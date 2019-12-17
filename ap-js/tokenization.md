# Tokenization

Tokenization in ACTUS Protocol is optional. It usually makes most sense for the _Beneficiary_ side of an asset \(the side that will receive the principal and/or interest payments after the initial exchange, i.e. the loan amount was paid\). 

ACTUS Protocol makes use of an implementation of [ERC-2222](https://github.com/ethereum/EIPs/issues/2222) to efficiently distribute cash flows to token holders.

{% hint style="info" %}
ACTUS Protocol currently only supports tokenization of the Beneficary side of an asset
{% endhint %}

### Example

Alice lends 100 DAI to Bob. Bob pays the DAI back over the course of 1 year. Each month he pays a percentage of the principal + interest.

Alice tokenizes her side of the asset. She has multiple options:

* She tokenizes all cash flows of the asset together. For instance, 100 Tokens are issued. Each token represents 1% of the future cash flow of the asset \(principal payments + interest payments\)
* She tokenizes interest payments and principal payments separately. 100 Principal Tokens and 100 Interest Tokens are created.

Let's assume the latter case. Now Alice can sell the Principal & Interest tokens indiviually on an ERC20 compatible market. Potential buyers can look at the underlying asset and price the tokens according to the outstanding cash flow and their individual risk assessment.

### Workflow

* Issue an AP Asset
* Use `asset.tokenizeBeneficiary()` to tokenize the beneficiary side

```typescript
const distributorAddress = await asset.tokenizeBeneficiary();
```

By default all cash-flows are included when an asset is tokenized. In order to tokenize individual cash-flows, please look at the [`TokenizationFactory()`](https://github.com/atpar/ap-monorepo/blob/MS1/packages/ap-contracts/contracts/Tokenization/TokenizationFactory.sol) in _ap-contracts_.

For more information please refer to [`tokenizeBeneficiary()`](https://ap-js.actus-protocol.io/classes/asset.html#tokenizebeneficiary) in the _AP.js_ documentation.



