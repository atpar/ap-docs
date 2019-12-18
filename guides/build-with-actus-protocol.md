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

* [yarn](https://yarnpkg.com/lang/en/docs/install/#debian-stable)

### Step 1: Add ap.js to your project

```bash
mkdir ap-tutorial && cd ap-tutorial
yarn init -y # initalize a default project
yarn add @atpar/ap.js 
```

### Step 2: Initialize the ACTUS Protocol library

```typescript
import Web3 from 'web3.js'; 
import { AP } from './ap.js';

// connecting to Görli Testnet via infura
const web3 = new Web3(new Web3.providers.Web3SocketProvider('wss://goerli.infura.io/ws/v3/<PROJECT_ID>'));

const defaultAccount = (await web3.eth.getAccounts())[0];

const ap = await AP.init(web3, defaultAccount);
```

