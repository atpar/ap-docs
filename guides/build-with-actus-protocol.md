---
description: >-
  This guide explains how to set up actus Protocol and develop with it. It's the
  ACTUS Protocol "Hello World" equivalent.
---

# Getting started

{% hint style="info" %}
The provided instructions have been tested on _Ubuntu_. They will likely work in a similar way on other  distros.
{% endhint %}

This guide assumes that you are working against the _Goerli deployment_ of ACTUS Protocol. For a custom deployment, see the custom deployment guide.

### Step 0: Install prerequisites

* git
* [yarn](https://yarnpkg.com/lang/en/docs/install/#debian-stable)

### Step 1: Add ap.js to your project

```bash
mkdir ap-tutorial && cd ap-tutorial
yarn init -y # initalize a default project
yarn add @atpar/ap.js 
```

### Step 2: Initialize the ACTUS Protocol library

```typescript
import { AP, Asset, Order, APTypes } from './ap.js';

const addressBook: APTypes.AddressBook;

const ap = await AP.init(
  web3, 
  DEFAULT_ACCOUNT,
  addressBook // optional addresses specified in ap-contracts for the current network
);
```

