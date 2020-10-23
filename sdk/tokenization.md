# Tokenization

> Tokenization in ACTUS Protocol means that for a side of an ACTUS contract ownership in cash flows is represented through ownership of an Ethereum ERC-20 compatible token. 
>
> Token holders receive a percentage of the cash flow, proportional to the fraction of the token supply they own. They can withdraw their balances at any time.

Tokenization is optional. It usually makes most sense for the _Beneficiary_ side of an asset \(the side that will receive the principal and/or interest payments after the initial exchange, i.e. the loan amount, was paid\). 

ACTUS Protocol makes use of an implementation of [ERC-2222](https://github.com/ethereum/EIPs/issues/2222) to efficiently distribute cash flows to token holders.

### Example

Alice lends 100 DAI to Bob. Bob pays the DAI back over the course of 1 year.  Each month he pays a percentage of the principal + interest.

Alice is the beneficiary and tokenizes her side of the asset. She has multiple options:

* She tokenizes all cash flow types of the asset together. For instance, she decides to issue 100 tokens. Each individual token represents exactly 1% of the future cash flow of the asset \(principal payments + interest payments\).
* She tokenizes interest payments and principal payments separately. 100 Principal Tokens and 100 Interest Tokens are created, each representing 1% of the respective cash flow type.

Let's assume the latter case. Now Alice can sell the principal & interest tokens individually on an ERC-20 compatible market. Potential buyers can look at the underlying asset and price the tokens according to the outstanding cash flow and their individual risk assessment.

### Workflow

* Deploy a token contract, e.g. an ERC-2222 or just an ERC-20 contract
* Set the contract's address as the beneficiary of an asset
* Issue the asset

By default all cash-flows are included when an asset is tokenized.



