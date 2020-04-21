---
description: Retrieve information about the state of ACTUS Protocol assets vie GraphQL
---

# Overview

The easiest way to access on-chain information about ACTUS Protocol Assets is to use GraphQL via TheGraph. We have set up a subgraph for the _Goerli_ deployment of ACTUS Protocol:

{% embed url="https://thegraph.com/explorer/subgraph/atpar/actus-protocol-goerli" %}

In addition to the below queries, you can find some executable examples on the [playground](https://thegraph.com/explorer/subgraph/atpar/actus-protocol?selected=playground). 

![Query examples](../.gitbook/assets/image%20%284%29.png)

## Schema

The top level entities of the GraphQL schema are as follows:

* Asset
* Template 
* Period 
* Contract
* Reference 
* TemplateSchedule 
* AssetOwnership 
* State 
* Schedule 
* Event 

To get a full understanding of the information you can retrieve via TheGraph, please check out the schema on the [subgraph page](https://thegraph.com/explorer/subgraph/atpar/actus-protocol) and look at the [subgraph definition](https://github.com/atpar/ap-subgraph).

## Endpoint

The GraphQL endpoint is

[`https://api.thegraph.com/subgraphs/name/atpar/actus-protocol`](https://api.thegraph.com/subgraphs/name/atpar/actus-protocol)\`\`

Method: POST

To test out your queries, we recommend to use a tool like [Postman](https://learning.postman.com/docs/postman/sending-api-requests/graphql/).

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
        "assetId": "0x225d599efc5681f4539ec17da64b6d8f550780b2841f2bbd39a01440315ec246"
      },
      {
        "assetId": "0x5f000e8e2afc30d56174ba7accc4891f793eba44533898db62b61d053208549a"
      },
      {
        "assetId": "0xeb54e8cc07786c3fc0b66d75e3a93d3aaebb4cfc44f9444986c56f0d01aa4206"
      },
      {
        "assetId": "0xee5ec4fb2ba2fb046dd7d2b3eef5259c53c997a20bd2ec9d4a832903f5114bd9"
      }
    ]
  }
}Get 
```
{% endtab %}
{% endtabs %}

### Get Template IDs

Receive template IDs 6-10.

{% tabs %}
{% tab title="Query" %}
```graphql
{
  templates(first: 5, skip: 5) {
    templateId
  }
}
```
{% endtab %}

{% tab title="Example response" %}
```javascript
{
  "data": {
    "templates": [
      {
        "templateId": "0x2e437d1c1c9ce0dcb77ea06377bce754c27db8cdbbe14987fbcafc0fcf17759e"
      },
      {
        "templateId": "0x33aa20cd7e6d7de7a298af850a739cbac16b7f300269a44a52cc6e6d78d40a1b"
      },
      {
        "templateId": "0x35d7177d483302d211722944109b1aa2a8c001b76beebb708f0890ddafb3e9b7"
      },
      {
        "templateId": "0x3e74682a49bc2b245d826f38042ec0fcb5ea368dd9f513ed04876937afdbed80"
      },
      {
        "templateId": "0x479dea92a6d45cf627f28db93442f575b04ca7b67a598fd408c1053bb167b472"
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
        assetId: "0x225d599efc5681f4539ec17da64b6d8f550780b2841f2bbd39a01440315ec246"
      }) 
    {
    assetId
    templateId
    engine
    actor
    ownership {
      creatorObligor
      creatorBeneficiary
      counterpartyObligor
      counterpartyBeneficiary
    }
    lifecycleTerms {
      notionalPrincipal
      nominalInterestRate
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
        "actor": "0x34f39cc7730462643dfc42f34a7a467720675099",
        "assetId": "0x225d599efc5681f4539ec17da64b6d8f550780b2841f2bbd39a01440315ec246",
        "engine": "0x4a97e3211fe60e09801b5d60d1a04db5b509504f",
        "lifecycleTerms": {
          "nominalInterestRate": "35000000000000000",
          "notionalPrincipal": "153000000000000000000"
        },
        "ownership": {
          "counterpartyBeneficiary": "0xb1495069f8d780b0c4123e96b0b6bb0217048c09",
          "counterpartyObligor": "0xb1495069f8d780b0c4123e96b0b6bb0217048c09",
          "creatorBeneficiary": "0x2c390ca49cefb345330cfe86a518b7de85e577fa",
          "creatorObligor": "0x2c390ca49cefb345330cfe86a518b7de85e577fa"
        },
        "state": {
          "statusDate": "1579019453"
        },
        "templateId": "0x5f8942d1f0a041edbad7a500e79f0f57988e491836b17a2abb248a6fab3e0d52"
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}

### Get Template Data

Retrieve the first 10 templates

{% tabs %}
{% tab title="Query" %}
```graphql
{
  templates(first: 1) {
    templateId
    templateTerms {
      calendar
      contractRole
      dayCountConvention
      businessDayConvention
      endOfMonthConvention
      scalingEffect
      penaltyType
      feeBasis
      creditEventTypeCovered
      currency
      settlementCurrency
      marketObjectCodeRateReset
      statusDateOffset
      maturityDateOffset
      feeAccrued
      accruedInterest
      rateMultiplier
      feeRate
      nextResetRate
      penaltyRate
      priceAtPurchaseDate
      nextPrincipalRedemptionPayment
      gracePeriod {
        i
        p
        isSet
      }
      delinquencyPeriod {
        i
        p
        isSet
      }
      periodCap
      periodFloor
    }
    templateSchedule {
      nonCyclicSchedule
      cyclicIPSchedule
      cyclicPRSchedule
      cyclicSCSchedule
      cyclicRRSchedule
      cyclicFPSchedule
      cyclicPYSchedule
    }
  }
}
```
{% endtab %}

{% tab title="Example response" %}
```graphql
{
  "data": {
    "templates": [
      {
        "templateId": "0x00f912e7a40f034981737960d3832c6e551a97ca9bdd77bb66af9d84d47e9493",
        "templateSchedule": {
          "cyclicFPSchedule": [],
          "cyclicIPSchedule": [
            "0x0800000000000000000000000000000000000000000000000000000000282170",
            "0x08000000000000000000000000000000000000000000000000000000004d0b70",
            "0x0800000000000000000000000000000000000000000000000000000000786450"
          ],
          "cyclicPRSchedule": [],
          "cyclicPYSchedule": [],
          "cyclicRRSchedule": [],
          "cyclicSCSchedule": [],
          "nonCyclicSchedule": [
            "0x0500000000000000000000000000000000000000000000000000000000000001",
            "0x0a00000000000000000000000000000000000000000000000000000000786450"
          ]
        },
        "templateTerms": {
          "accruedInterest": "0",
          "businessDayConvention": 0,
          "calendar": 0,
          "contractRole": 0,
          "creditEventTypeCovered": 0,
          "currency": "0x0000000000000000000000000000000000000000",
          "dayCountConvention": 1,
          "delinquencyPeriod": {
            "i": "0",
            "isSet": false,
            "p": 0
          },
          "endOfMonthConvention": 1,
          "feeAccrued": "0",
          "feeBasis": 0,
          "feeRate": "0",
          "gracePeriod": {
            "i": "0",
            "isSet": false,
            "p": 0
          },
          "marketObjectCodeRateReset": "0x0000000000000000000000000000000000000000000000000000000000000000",
          "maturityDateOffset": "7890000",
          "nextPrincipalRedemptionPayment": "0",
          "nextResetRate": "0",
          "penaltyRate": "0",
          "penaltyType": 0,
          "periodCap": "1",
          "periodFloor": "0",
          "priceAtPurchaseDate": "0",
          "rateMultiplier": "0",
          "scalingEffect": 1,
          "settlementCurrency": "0x0000000000000000000000000000000000000000",
          "statusDateOffset": "31"
        }
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}



