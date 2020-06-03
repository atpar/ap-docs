---
description: >-
  This guide explains how to set up ACTUS Protocol and develop with it. It's the
  ACTUS Protocol "Hello World" equivalent.
---

# Getting started

{% hint style="info" %}
The provided instructions have been tested on macOS and Ubuntu. If you run into any issues with your setup - let us now on Discord.
{% endhint %}

This guide uses the current version of ACTUS Protocol smart contracts deployed on _Goerli  Testnet_.

### Install prerequisites

You should be on a linux compatible shell with basic dev tools like git installed. The ACTUS Protocol dev environment is most easily setup with yarn.

* Install [node](https://nodejs.org/en/) e.g. via [nvm](https://github.com/nvm-sh/nvm) \(tested on version 10.16.0\)
* Install [yarn](https://yarnpkg.com/lang/en/docs/install/#debian-stable) e.g. as a global npm package via `npm install yarn --global`

### Create a new project

In your shell, execute the following commands to create a new project and to install `ap.js`.

```bash
mkdir ap-tutorial && cd ap-tutorial
yarn init -y # initalize a default project
yarn add @atpar/ap.js 
```

### Getting started with ap.js

To initialize the project, set your web3 provider \(e.g. [Infura](https://infura.io/), or a local Ethereum node\) and the default account which should be used for signing transactions and orders.

```typescript
import Web3 from 'web3.js'; 
import { AP } from '@atpar/ap.js';

// connecting to Görli Testnet via infura
const web3 = new Web3(new Web3.providers.Web3SocketProvider('wss://goerli.infura.io/ws/v3/<PROJECT_ID>'));

const defaultAccount = (await web3.eth.getAccounts())[0];

const ap = await AP.init(web3, defaultAccount);
```

