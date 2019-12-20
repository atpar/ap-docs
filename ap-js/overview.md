---
description: >-
  AP.js is a typescript library for interacting with the ACTUS Protocol smart
  contracts. It allows developers to create and manage ACTUS assets.
---

# Overview

### Important Resources

* [GitHub Repository](https://github.com/atpar/ap-monorepo/tree/MS1/packages/ap.js)
* AP.js [API Documentation](https://ap-js.actus-protocol.io/)

### Usage

```bash
yarn add @atpar/ap.js
```

#### Setup

Initializing the ACTUS Protocol library.

```typescript
import Web3 from 'web3.js'; 
import { AP, Asset, Order, APTypes } from './ap.js';

// connecting to Görli Testnet via infura
const web3 = new Web3(new Web3.providers.Web3SocketProvider('wss://goerli.infura.io/ws/v3/<PROJECT_ID>'));

const defaultAccount = (await web3.eth.getAccounts())[0];

const addressBook: APTypes.AddressBook;

const ap = await AP.init(
  web3,
  defaultAccount,
  addressBook // optional pass custom address of ap-contracts to ap.js
);
```

#### Order

`Order` contains methods for creating orders and issuing assets from a co-signed orders.

```typescript
const orderParams: OrderParams = {
  termsHash: string; // hash of the entire terms object of the asset
  templateId: string; // id of the template which this asset should be based on
  customTerms: CustomTerms; // CustomTerms of the asset
  ownership: AssetOwnership; // ownership of the asset
  expirationDate: string; // timestamp of when this order expires
  engine: string; // address of the ACTUS Engine for the asset 
  enhancement_1?: { // optional object describing the first enhancement
    termsHash: string; // hash of the entire terms object of the first enhancement
    templateId: string; // id of the template the first enhancment should based on
    customTerms: CustomTerms; // CustomTerms of the first enhancement
    ownership: AssetOwnership;  // ownership of the first enhancement
    engine: string; // address of the ACTUS Engine for the first enhancement
  } | null;
  enhancement_2?: { // optional object describing the second enhancement
    termsHash: string; // hash of the entire terms object of the second enhancement
    templateId: string; // id of the template the second enhancment should based on
    customTerms: CustomTerms; // CustomTerms of the second enhancement
    ownership: AssetOwnership;  // ownership of the second enhancement
    engine: string; // address of the ACTUS Engine for the second enhancement
  } | null;
};

const order = Order.create(ap, orderParams);
```

Serializing an `Order` as `OrderData`

```typescript
const orderData: OrderData = order.serializeOrder();
```

Instantiate an `Order` from `OrderData`.

```typescript
const order = Order.load(ap, orderData);
```

Signing an order \(as creator or counterparty obligor\).

```typescript
await order.signOrder();
```

Issue a new asset from an co-signed order \(requires both signatures\).

```typescript
await order.issueAssetFromOrder();
```

#### Asset

`Asset` is a wrapper around `AP.js` APIs to make the creation and the lifecycle management of an ACTUS asset easier.

Loading an Asset given its AssetId from the Asset Registry.

```typescript
const asset = await Asset.load(ap, ASSET_ID);
```

Retrieve information of the asset such as the terms, the state or the ownership.

```typescript
const terms = await asset.getTerms();
```

Retrieve the projected schedule of the asset \(does not contain unscheduled events such as CD\)

```typescript
const schedule = await asset.getSchedule();
```

Settlement of obligations: The next obligation is the most immediate obligation which is not yet paid off.

```typescript
// event type, schedule time of the event
const event = ap.utils.decodeEvent(await asset.getNextEvent());
// payment information of the event
const payment = await asset.getNextPayment();
```

Progressing the state of the asset. Requires that the Asset Actor has sufficient allowance to settle the obligation of the pending event. If there are unsettled obligation for the pending event, the actor will transition the state of the asset to a non-performant state.

```typescript
await asset.progress(); // progresses the state to the current block timestamp
```

Tokenizing the one of the beneficiaries of the asset. Tokenizes the beneficary \(respective to the default accounts ownership of the asset\) by deploying a new Funds Distribution Token smart contract.

```typescript
const distributorAddress = await asset.tokenizeBeneficiary();
```

### API Overview

Also see the [API Documentation](https://ap-js.actus-protocol.io/)

| API | Description |
| :--- | :--- |
| Contracts | wrapper around the ACTUS Protocol smart contracts |
| Signer | interact with actus-solidity engines - retrieve terms, state and the current EventId of a registered asset |
| Utils | utility methods for conversions, constants, creating signatures and handling schedules |



