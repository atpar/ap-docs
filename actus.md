---
description: >-
  Solidity implementation of ACTUS Contract Types
  (https://www.actusfrf.org/algorithmic-standard)
---

# ACTUS

ACTUS Protocol \([GitHub](https://github.com/atpar/ap-monorepo/tree/master)\) contains a solidity implementation of the ACTUS standard. ACTUS was created by the [ACTUS Foundation](https://www.actusfrf.org). 

> The goal of ACTUS is to break down the diversity in financial instruments into a manageable number of cash flow patterns – so called Contract Types \(CT\).

You can find the complete specifications of the two parts of the standard, the _ACTUS Data Standard_ and the _ACTUS Algorithmic Standard_ on [GitHub](https://github.com/actusfrf).

In [`protocol`](https://github.com/atpar/ap-monorepo/tree/master/packages/protocol) we ported the Standards to solidity and are incrementally implementing ACTUS contract types. Currently the following contract types have been implemented:

* **ANN** - Annuity: Used for instruments where interest and principal are paid back over the lifetime of the asset.
* **CEG** - Guarantee: Creates a relationship between a guarantor, an obligee and a debtor, moving the exposure from the debtor to the guarantor.
* **CEC** - Collateral: Creates a relationship between a collateral an obligee and a debtor, covering the exposure from the debtor with the collateral.
* **CERTF** - Certificates
* **PAM** - Principal at Maturity: Used e.g. for assets where interest is paid over the lifetime but the principal is paid at the end of the schedule.
* **STK** - Stocks

The ACTUS implementation in Solidity can be used independently for creating ACTUS instruments on Ethereum but also is the foundational component for the protocol.





