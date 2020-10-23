---
description: Retrieve information about the state of ACTUS Protocol assets using GraphQL
---

# Overview

The easiest way to access on-chain information about ACTUS Protocol Assets is to use GraphQL via TheGraph. We have set up subgraphs for the _Goerli_ & _Rinkeby_ deployments of ACTUS Protocol. You can use these pages also to test your queries.

{% embed url="https://thegraph.com/explorer/subgraph/atpar/actus-protocol-goerli" %}

{% embed url="https://thegraph.com/explorer/subgraph/atpar/actus-protocol-rinkeby" %}

In addition to the below queries, you can find some executable examples in the TheGraph interface. You can also use the TheGraph website to test your queries.

![Query examples](../.gitbook/assets/image%20%284%29.png)

## Schema

The top level entities of the GraphQL schema are as follows:

* Asset
* Schedule
* State
* DataPoint 
* DataSet 
* Holder 
* Distributor 
* Period 
* Cycle 
* ContractReference 
* AssetOwnership 
* ANNAsset 
* CECAsset 
* CEGAsset 
* CERTFAsset 
* PAMAsset 
* DvPSettlementData 

To get a full understanding of the information you can retrieve via TheGraph, please check out the schema on the subgraph page and look at the [subgraph definition](https://github.com/atpar/ap-subgraph).

## Endpoint

The GraphQL endpoint is

[`https://api.thegraph.com/subgraphs/name/atpar/actus-protocol-rinkeby`  
](https://api.thegraph.com/subgraphs/name/atpar/actus-protocol-rinkeby
)[`https://api.thegraph.com/subgraphs/name/atpar/actus-protocol-goerli`](https://api.thegraph.com/subgraphs/name/atpar/actus-protocol-goerli
)

Method: POST

### Get Asset IDs

Receive the first 5 asset IDs

{% tabs %}
{% tab title="Query" %}
```graphql
{
  assets(first: 5) {
    assetId
  }
}
```
{% endtab %}

{% tab title="Example response" %}
```javascript
{
  "data": {
    "assets": [
      {
        "assetId": "0x0ac2f5b794130c2cea06ff17ef82b3915b44428afbf9ae7a47793dd917ee622c"
      },
      {
        "assetId": "0x114594f5362b70c295aab5e2c4a8a5244f9549e9c5b490a665a6a36e9613d947"
      },
      {
        "assetId": "0x190c36897108177fe3fb7d35e1be536bb5a095e201726fbd2d9bcd7f9cbc88e2"
      },
      {
        "assetId": "0x19dd7a3fb650940f23364a1acc3defcac11321ea8a4c5047c16bafef8104b736"
      },
      {
        "assetId": "0x3a7cf8e04f3f279b98ea02004ea2dc1be446130e090985da2721aa72790fb365"
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}

### Get Asset Data

Get asset data for a specific asset ID

{% tabs %}
{% tab title="Query" %}
```graphql
{
  assets(
    where: 
      {
        assetId: "0x0ac2f5b794130c2cea06ff17ef82b3915b44428afbf9ae7a47793dd917ee622c"
      }) 
    {
    assetId
    engine
    actor
    ownership {
      creatorObligor
      creatorBeneficiary
      counterpartyObligor
      counterpartyBeneficiary
    }
     schedule{
      events
    }
    state {
      statusDate
    }
  }
}
```
{% endtab %}

{% tab title="Example response" %}
```graphql
{
  "data": {
    "assets": [
      {
        "actor": "0x5eae9ff56ad6ced8b060a9072f2b4dbf11136924",
        "assetId": "0x0ac2f5b794130c2cea06ff17ef82b3915b44428afbf9ae7a47793dd917ee622c",
        "engine": "0xa15cee3298c48ace9c73a7e9f11c33ec936ffc80",
        "ownership": {
          "counterpartyBeneficiary": "0xc056af70170342dcc2fdaed5f3087cbd551f2cb4",
          "counterpartyObligor": "0xc056af70170342dcc2fdaed5f3087cbd551f2cb4",
          "creatorBeneficiary": "0xdaee6d219ad6d151c4a68c35cf910c67d8dbed41",
          "creatorObligor": "0xdaee6d219ad6d151c4a68c35cf910c67d8dbed41"
        },
        "schedule": {
          "events": [
            "0x020000000000000000000000000000000000000000000000000000005f254e08",
            "0x14000000000000000000000000000000000000000000000000000000612e0e88"
          ]
        },
        "state": {
          "statusDate": "1596280328"
        }
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}



