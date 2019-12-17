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

{% hint style="success" %}
**Looking for assistance?**   
Our helpful team is available to chat on [Discord](https://discord.gg/WdAhDYq)!
{% endhint %}

ACTUS Protocol is a smart contract system and Typescript library for issuing and servicing financial assets on Ethereum. It is build on top of `actus-solidity` a free and open-source implementation of the [ACTUS](https://www.actusfrf.org/) standard. 

All ACTUS assets have a unified term sheet and a clear and understandable schedule. External data, such as interest rates are supported through external market objects which can be connected to oracles. Assets can have credit enhancements such as on-chain collateral or legal guarantees.

ACTUS Assets are registered in the AssetRegistry. They progress through their life-cycle using a state machine based on their schedule. The schedule is generated directly from the soldity implementation of ACTUS, guaranteeing a common understanding about _who pays what to whom and when_.

![ACTUS Protocol](.gitbook/assets/image%20%284%29.png)

**Core features:**

* Issue ACTUS assets
* Progress ACTUS assets throughout their life-cycle
* Tokenize cash flows of ACTUS assets

## Components

### [`actus-solidity`](https://github.com/atpar/actus-solidity)

A solidity implementation of the ACTUS standard. ACTUS was created by the [ACTUS Foundation](https://www.actusfrf.org). 

> The goal of ACTUS is to break down the diversity in financial instruments into a manageable number of cash flow patterns – so called Contract Types \(CT\).

You can find the complete specifications of the two parts of the standard, the _ACTUS Data Standard_ and the _ACTUS Algorithmic Standard_ on [GitHub](https://github.com/actusfrf).

In `actus-solidity` we ported the Standards to solidity and are incrementally implementing ACTUS contract types. Currently the following contract types have been implemented:

* **PAM** - Principal at Maturity: Used e.g. for assets where interest is paid over the lifetime but the principal is paid at the end of the schedule.
* **ANN** - Annuity: Used for instruments where einterest and principal are paid back over the lifetime of the asset.
* **CEG** - Guarantee: Ceates a relationship between a guarantor, an obligee and a debtor, moving the exposure from the debtor to the guarantor.
* **CEC** - Collateral: Creates a relationship between a collateral an obligee and a debtor, covering the exposure from the debtor with the collateral.

`actus-solidity` can be used independently for creating ACTUS instruments on Ethereum but also is the foundational component for ACTUS Protocol.

### [`ap-contracts`](https://github.com/atpar/ap-monorepo/tree/MS1/packages/ap-contracts)

`ap-contracts` is a collection of solidity contracts that comprise the ACTUS Protocol smart contract system. It depends on `actus-solidity` and uses ACTUS definitions and ACTUS engines for issuing and progressing ACTUS Protocol assets.

Main Components:

* Core - Includes 
* Issuance
* Tokenization
* external



### [`ap.js`](https://github.com/atpar/ap-monorepo/tree/MS1/packages/ap.js)

safdsdafsd

