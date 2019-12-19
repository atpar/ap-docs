---
description: >-
  This guide explains how to set up actus Protocol and develop with it. It's the
  ACTUS Protocol "Hello World" equivalent.
---

# Getting started

{% hint style="info" %}
The provided instructions have been tested on _Ubuntu_. They will likely work in a similar way on other  distros.
{% endhint %}

This guide assumes that you are working against the _Goerli deployment_ of ACTUS Protocol.

### Install prerequisites

You should be on a linux compatible shell with basic dev tools like git installed. The ACTUS Protocol dev environment is most easily setup with yarn.

* Install [yarn](https://yarnpkg.com/lang/en/docs/install/#debian-stable)

### Add ap.js to your project

In your shell, execute the following commands to create a simple project and add `ap.js` to it.

```bash
mkdir ap-tutorial && cd ap-tutorial
yarn init -y # initalize a default project
yarn add @atpar/ap.js 
```

### Initialize the ACTUS Protocol library

To initialize the project, tell your web3 object what provider it should use \(e.g. infura, or a local Ethereum node\). The default account will be used for signing e.g. orders.

```typescript
import Web3 from 'web3.js'; 
import { AP } from './ap.js';

// connecting to Görli Testnet via infura
const web3 = new Web3(new Web3.providers.Web3SocketProvider('wss://goerli.infura.io/ws/v3/<PROJECT_ID>'));

const defaultAccount = (await web3.eth.getAccounts())[0];

const ap = await AP.init(web3, defaultAccount);
```

