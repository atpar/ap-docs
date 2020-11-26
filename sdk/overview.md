---
description: >-
  The Typescript SDK allows developers to easily create and manage ACTUS assets
  by simplifying the interaction with the ACTUS Protocol smart contracts.
---

# Overview

### Usage

Install the package via:

```bash
yarn add @atpar/protocol
```

#### Setup

Initializing the Typescript SDK.

```typescript
import Web3 from 'web3.js'; // v1.2.4
import { AP } from '@atpar/protocol';

// connecting to Rinkeby Testnet via infura
const web3 = new Web3(new Web3.providers.Web3SocketProvider('wss://rinkeby.infura.io/ws/v3/<PROJECT_ID>'));

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



