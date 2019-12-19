---
description: This page gives a quick introduction into main components of ACTUS Protocol
---

# ACTUS Protocol Introduction

{% hint style="warning" %}
WORK IN PROGRESS  
This documentation is momentarily being created.
{% endhint %}

{% hint style="danger" %}
The ACTUS Protocol has not been audited, yet. Don't put your funds at risk!
{% endhint %}

ACTUS Protocol is a smart contract system and Typescript library for issuing and servicing financial assets on Ethereum. It is build on top of `actus-solidity` a free and open-source implementation of the [ACTUS](https://www.actusfrf.org/) standard. 

All ACTUS assets have a unified term sheet and a clear and understandable schedule. External data, such as interest rates are supported through external market objects which can be connected to oracles. Assets can have credit enhancements such as on-chain collateral or legal guarantees.

ACTUS Assets are registered in the AssetRegistry. They progress through their life-cycle using a state machine based on their schedule. The schedule is generated directly from the soldity implementation of ACTUS, guaranteeing a common understanding about _who pays what to whom and when_.

![ACTUS Protocol](.gitbook/assets/image%20%281%29.png)

**Core features:**

* Issue ACTUS assets
* Progress ACTUS assets throughout their life-cycle
* Tokenize cash flows of ACTUS assets

{% hint style="success" %}
**Looking for assistance?**   
Our helpful team is available to chat on [Discord](https://discord.gg/WdAhDYq)!
{% endhint %}

## Components

### [`actus-solidity`](https://github.com/atpar/actus-solidity)

\[1 paragraph\]

### [`ap-contracts`](https://github.com/atpar/ap-monorepo/tree/MS1/packages/ap-contracts)

`ap-contracts` is a collection of solidity contracts that comprise the ACTUS Protocol smart contract system. It depends on `actus-solidity` and uses ACTUS definitions and ACTUS engines for issuing and progressing ACTUS Protocol assets.

### [`ap.js`](https://github.com/atpar/ap-monorepo/tree/MS1/packages/ap.js)

\[1 paragraph\]

