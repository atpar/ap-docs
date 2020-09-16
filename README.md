---
description: >-
  ACTUS Protocol (AP) is a smart contract system and Typescript library for
  issuing and servicing financial assets on Ethereum.
---

# Introduction



{% hint style="info" %}
This software has not been audited, yet. Don't put your funds at risk!
{% endhint %}

![](.gitbook/assets/image%20%281%29.png)



**Core features:**

* Issue financial assets
* Progress assets throughout their life-cycle
* Tokenize cash flows of assets

AP is build on top of [`actus-solidity`](https://github.com/atpar/ap-monorepo/tree/master/packages/actus-solidity) a free and open-source implementation of the [ACTUS](https://www.actusfrf.org/) standard. 

All ACTUS assets have a unified term sheet and a clear and well-defined schedule. External data, such as changing interest rates are supported through external market objects which can be connected to oracles. Assets can have credit enhancements such as on-chain collateral or legal guarantees.

ACTUS Assets are registered in an asset registry. They are progressed through their life-cycle according to their schedule. An Asset's schedule, which is the basis for the state machine, is derived from its terms using the solidity implementation of ACTUS, guaranteeing a common understanding about _who owes what to whom and when_.

{% hint style="success" %}
**Looking for assistance?**   
Our helpful team is available to chat on [Discord](https://discord.gg/WdAhDYq)!
{% endhint %}

