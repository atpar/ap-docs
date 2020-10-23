---
description: >-
  The Typescript SDK allows developers to easily create and manage ACTUS assets
  by simplifying the interaction with the ACTUS Protocol smart contracts.
---

# Overview

### Usage

The protocol package is hosted on GitHub package and requires additional configuration. To configure npm or yarn to use the GitHub Package Registry see: [docs.github.com](https://docs.github.com/en/free-pro-team@latest/packages/using-github-packages-with-your-projects-ecosystem/configuring-npm-for-use-with-github-packages). After you configured the npm cli to access the GitHub Package Registry create a `.npmrc`file in the root of your project with following content: 

```typescript
@atpar:registry=https://npm.pkg.github.com
```

If you configured everything correctly you should be able to install the package via:

```bash
yarn add @atpar/protocol
```

#### Setup

Initializing the Typescript SDK.

```typescript
import Web3 from 'web3.js'; // v1.2.4
import { AP } from '@atpar/protocol';

// connecting to Görli Testnet via infura
const web3 = new Web3(new Web3.providers.Web3SocketProvider('wss://goerli.infura.io/ws/v3/<PROJECT_ID>'));

const defaultAccount = (await web3.eth.getAccounts())[0];

const addressBook: APTypes.AddressBook; // addresses are provided on GitHub

const ap = await AP.init(
  web3,
  addressBook
);
```

#### 

### API Overview

| API | Description |
| :--- | :--- |
| Contracts | wrapper around the ACTUS Protocol smart contracts |
| Utils | utility methods for conversions, constants, creating signatures and handling schedules |



