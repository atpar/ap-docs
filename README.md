---
description: Understand what ACTUS Protocol is all about and what its main features are
---

# Introduction

{% hint style="warning" %}
WORK IN PROGRESS  
This documentation is momentarily being created.
{% endhint %}

{% hint style="danger" %}
The ACTUS Protocol has not been audited, yet. Don't put your funds at risk!
{% endhint %}

![](.gitbook/assets/image%20%281%29.png)

ACTUS Protocol is a smart contract system and Typescript library for issuing and servicing financial assets on Ethereum. It is build on top of [`actus-solidity`](https://github.com/atpar/ap-monorepo/tree/master/packages/actus-solidity) a free and open-source implementation of the [ACTUS](https://www.actusfrf.org/) standard. 

All ACTUS assets have a unified term sheet and a clear and understandable schedule. External data, such as interest rates are supported through external market objects which can be connected to oracles. Assets can have credit enhancements such as on-chain collateral or legal guarantees.

ACTUS Assets are registered in an asset registry. They progress through their lifecycle using a state machine  that is based on their contract type. The schedule is generated directly from the soldity implementation of ACTUS, guaranteeing a common understanding about _who ows what to whom and when_.

**Core features:**

* Issue ACTUS assets
* Progress ACTUS assets throughout their lifecycle
* Tokenize cash flows of ACTUS assets

{% hint style="success" %}
**Looking for assistance?**   
Our helpful team is available to chat on [Discord](https://discord.gg/WdAhDYq)!
{% endhint %}

