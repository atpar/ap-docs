---
description: ACTUS terms for some example contracts
---

# Example Contract Terms

## Coupon-Paying Bond \(PAM\)

This product reflects an unsecured, fixed-rate coupon bearing bond with a 1 year lifetime. The product offers the investor a quarterly \(interest\) coupon payment.

The interest rate is 0.5% and the notional principal is 100k TUSD.

```javascript
{
   "contractType":"PAM",
   "calendar":"MF",
   "contractRole":"RPA",
   "dayCountConvention":"A360",
   "businessDayConvention":"CSMF",
   "endOfMonthConvention":"SD",
   "scalingEffect":"000",
   "penaltyType":"N",
   "feeBasis":"A",
   
   "currency":"0x6Ce7BFC48be104950D6506c7FC16486446a24261",
   "settlementCurrency":null,
   
   "marketObjectCodeRateReset":null,
   
   "contractDealDate":"2020-09-25T10:20:40.000Z",
   "statusDate":"2020-09-25T10:20:40.000Z",
   "initialExchangeDate":"2020-09-26T10:20:40.000Z",
   "maturityDate":"2021-09-25T10:20:40.000Z",
   "purchaseDate":null,
   "capitalizationEndDate":null,
   "cycleAnchorDateOfInterestPayment":"2020-12-25T10:20:40.000Z"
   "cycleAnchorDateOfRateReset":null,
   "cycleAnchorDateOfScalingIndex":null,
   "cycleAnchorDateOfFee":null,
   
   "notionalPrincipal":"100000",
   "nominalInterestRate":"0.005",
   "accruedInterest":"0",
   "rateMultiplier":"0",
   "rateSpread":"0",
   "nextResetRate":"0",
   "feeRate":"0",
   "feeAccrued":"0",
   "penaltyRate":"0",
   "delinquencyRate":"0",
   "premiumDiscountAtIED":"0",
   "priceAtPurchaseDate":"0",
   
   "lifeCap":"0",
   "lifeFloor":"0",
   "periodCap":"0",
   "periodFloor":"0",
   
   "gracePeriod":"30D",
   "delinquencyPeriod":"6M",
   
   "cycleOfInterestPayment":"3M-",
   "cycleOfRateReset":"0D-",
   "cycleOfScalingIndex":"0D-",
   "cycleOfFee":"0D-",
}
```

## Amortizing Loan \(ANN\)

This product reflects an unsecured, amortizing fixed-rate loan. Principal and coupon are paid monthly to the investor. 

The interest rate is 0.5% and the notional principal is 100k TUSD. Both grace and delinquency periods have been defined.

```javascript
{
   "contractType":"ANN",
   "calendar":"MF",
   "contractRole":"RPA",
   "dayCountConvention":"A360",
   "businessDayConvention":"CSMF",
   "endOfMonthConvention":"SD",
   "scalingEffect":"000",
   "penaltyType":"N",
   "feeBasis":"A",
   
   "currency":"0x6Ce7BFC48be104950D6506c7FC16486446a24261",
   "settlementCurrency":null,
   
   "marketObjectCodeRateReset":null,
   
   "contractDealDate":"2020-09-02T10:53:26.000Z",
   "statusDate":"2020-09-02T10:53:26.000Z",
   "initialExchangeDate":"2020-09-03T10:53:26.000Z",
   "maturityDate":"2021-09-02T10:53:26.000Z",
   "purchaseDate":null,
   "capitalizationEndDate":null,
   
   "cycleAnchorDateOfInterestPayment":"2020-10-02T10:53:26.000Z",
   "cycleAnchorDateOfRateReset":null,
   "cycleAnchorDateOfScalingIndex":null,
   "cycleAnchorDateOfFee":null,
   "cycleAnchorDateOfPrincipalRedemption":"2020-10-02T10:53:26.000Z"
   
   "notionalPrincipal":"100000",
   "nominalInterestRate":"0.005",
   "accruedInterest":"0",
   "rateMultiplier":"0",
   "rateSpread":"0",
   "nextResetRate":"0",
   "feeRate":"0",
   "feeAccrued":"0",
   "penaltyRate":"0",
   "delinquencyRate":"0",
   "premiumDiscountAtIED":"0",
   "priceAtPurchaseDate":"0",
   "nextPrincipalRedemptionPayment":"2.6667",
   
   "lifeCap":"0",
   "lifeFloor":"0",
   "periodCap":"0",
   "periodFloor":"0",
   
   "gracePeriod":"5D",
   "delinquencyPeriod":"30D",

   "cycleOfInterestPayment":"1M-",
   "cycleOfRateReset":"0D-",
   "cycleOfScalingIndex":"0D-",
   "cycleOfFee":"0D-",
   "cycleOfPrincipalRedemption":"1M-",
}
```

## Performance Certificate on Underlying ￼\(CERTF\)

This product reflects an open-ended performance certificate on an exchange-traded, underlying asset. The product offers the investor a bi-monthly redemption option.

```javascript
TBD
```

## Single-Entity Credit Default Swap \(CEG\)

This product protects the buyer from a credit event on a single underlying instrument.

```javascript
{
   "contractType":"CEG",
   "calendar":"MF",
   "contractRole":"BUY",
   "dayCountConvention":"A360",
   "businessDayConvention":"CSMF",
   "endOfMonthConvention":"SD",
   "feeBasis":"A",
   "creditEventTypeCovered":"DF",
   
   "currency":"0x6Ce7BFC48be104950D6506c7FC16486446a24261",
   "settlementCurrency":null,
   
   "contractDealDate":"2020-10-01T14:29:24.000Z",
   "statusDate":"2020-10-01T14:29:24.000Z",
   "maturityDate":"2021-10-01T14:29:24.000Z",
   "purchaseDate":null,
   "cycleAnchorDateOfFee":null,
   
   "notionalPrincipal":"32",
   "delinquencyRate":"0",
   "feeAccrued":"0",
   "feeRate":"0",
   "priceAtPurchaseDate":"0",
   "coverageOfCreditEnhancement":"1",
   
   "gracePeriod":"5D",
   "delinquencyPeriod":"30D",
   
   "cycleOfFee":"0D-",
   
   "contractStructure":{
      "contractReference":[
         {
            "object":"0xa6203756524a554bf7d6cfe88a9ac415c83ed65d123227bb2026d936e5a4bcdf",
            "object2":"0x0000000000000000000000002194bd1c5f48eaccbdc2b894abe98afa116aced8",
            "type":"CID",
            "role":"COVE"
         },
         {
            "object":"0x0000000000000000000000000000000000000000000000000000000000000000",
            "object2":"0x0000000000000000000000000000000000000000000000000000000000000000",
            "type":"CNT",
            "role":"UDL"
         }
      ]
   }
}
```
