---
description: >-
  AP.js is a typescript library for interacting with the ACTUS Protocol smart
  contracts. It allows developers to create and manage ACTUS assets.
---

# Overview

### Resources

* \*\*\*\*[**GitHub Repository**](https://github.com/atpar/ap-monorepo/tree/MS1/packages/ap.js)\*\*\*\*
* \*\*\*\*[**API Documentation**](https://ap-js.actus-protocol.io/)\*\*\*\*

### Usage

```bash
yarn add @atpar/ap.js
```

#### Setup

Initializing the ACTUS Protocol library.

```typescript
import Web3 from 'web3.js'; 
import { AP } from '@atpar/ap.js';

// connecting to Görli Testnet via infura
const web3 = new Web3(new Web3.providers.Web3SocketProvider('wss://goerli.infura.io/ws/v3/<PROJECT_ID>'));

const defaultAccount = (await web3.eth.getAccounts())[0];

const addressBook: APTypes.AddressBook;

const ap = await AP.init(
  web3,
  addressBook // optional pass custom address of ap-contracts to ap.js
);
```

#### 

### API Overview

Also see the [API Documentation](https://ap-js.actus-protocol.io/)

| API | Description |
| :--- | :--- |
| Contracts | wrapper around the ACTUS Protocol smart contracts |
| Utils | utility methods for conversions, constants, creating signatures and handling schedules |



