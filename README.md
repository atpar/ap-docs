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

## [`actus-solidity`](https://github.com/atpar/actus-solidity)

A solidity implementation of the ACTUS Standard. ACTUS was created by the [ACTUS Foundation](https://www.actusfrf.org). 

> The goal of ACTUS is to break down the diversity in financial instruments into a manageable number of cash flow patterns – so called Contract Types \(CT\).

You can find the complete specifications of the two parts of the standard, the _ACTUS Data Standard_ and the _ACTUS Algorithmic Standard_ on [GitHub](https://github.com/actusfrf).

In `actus-solidity` we ported the Standards to solidity and are incrementally implementing ACTUS contract types. Currently the following contract types have been implemented:

* **PAM** - Principal at Maturity: Used e.g. for assets where interest is paid over the lifetime but the principal is paid at the end of the schedule.
* **ANN** - Annuity: Used for instruments where einterest and principal are paid back over the lifetime of the asset.
* **CEG** - Guarantee: Ceates a relationship between a guarantor, an obligee and a debtor, moving the exposure from the debtor to the guarantor.
* **CEC** - Collateral: Creates a relationship between a collateral an obligee and a debtor, covering the exposure from the debtor with the collateral.

`actus-solidity` can be used independently for creating ACTUS instruments on Ethereum but also is the foundational component for ACTUS Protocol.

## [`ap-contracts`](https://github.com/atpar/ap-monorepo/tree/MS1/packages/ap-contracts)

`ap-contracts` is a collection of solidity contracts that comprise the ACTUS Protocol smart contract system. It depends on `actus-solidity` and uses ACTUS definitions and ACTUS engines for issuing and progressing ACTUS Protocol assets.

Main Components:

* Core - Includes 
* Issuance
* Tokenization
* external



## [`ap.js`](https://github.com/atpar/ap-monorepo/tree/MS1/packages/ap.js)

safdsdafsd

