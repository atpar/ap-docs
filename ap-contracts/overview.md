---
description: ACTUS Protocol smart contract system
---

# Overview

### Resources

* \*\*\*\*[**GitHub Repository**](https://github.com/atpar/ap-monorepo/tree/master/packages/ap-contracts)\*\*\*\*
* \*\*\*\*[**API Docs** ](https://github.com/atpar/ap-monorepo/tree/master/packages/ap-contracts/docs/)\*\*\*\*

`ap-contracts` is a collection of solidity contracts that comprise the ACTUS Protocol smart contract system. It depends on `actus-solidity` and uses ACTUS definitions and ACTUS engines for issuing and progressing ACTUS Protocol assets.





## The Term sheet

In ACTUS Protocol we have defined subsets of the full [ACTUS contract term sheet](https://github.com/actusfrf/actus-dictionary/blob/master/actus-dictionary-terms.json). Using these subsets increases on-chain efficiency and enables the template system of ACTUS Protocol.

**Terms:** The entire ACTUS compliant terms object. It is comprised of LifecycleTerms attributes, GeneratingTerms attributes and additional „meta“ attributes \(the latter two are not stored on-chain\).

**GeneratingTerms:** Contains only those attributes that are necessary for generating schedules \(also not stored on-chain\).

**LifecycleTerms:** Contains only attributes used on-chain for evaluating the POF and STF and in the AssetActor \(e.g. for generating unscheduled events, settling obligations, enhancements\). Can be derived from TemplateTerms and CustomTerms objects.

**TemplateTerms:** A modified subset of the LifecycleTerms object containing template specific attributes. All date attributes are defined as offsets instead of absolute date values. Attribute values equal to 0 are interpreted as “not set”, they are not shifted by anchor date.

**CustomTerms:** A modified subset of LifecycleTerms object containing asset specific attributes and an additional anchorDate attribute used to derive the actual date values from date offsets defined in the TemplateTerms object. GeneratingTerms and CustomTerms are mutually exclusive.

