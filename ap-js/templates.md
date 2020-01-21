# Templates

Assets have to be based on an already registered template \(see list of registered Templates on Görli Testnet below\). 

A template is comprises a set of `TemplateTerms` \(see. ...\) and `TemplateSchedules`. `TemplateSchedules` are a set of event type specific arrays containing raw events with relative timestamp \(or offsets\). In the `CustomTerms` of the asset the `anchor date` attribute is used to calculate the actual schedule time.

Anyone is able to register new  templates. `ap.js` provides methods for generating  `TemplateTerms` and `TemplateSchedules`from an ACTUS terms object.  

The number of events for `TemplateSchedules` is bound by the block gas limit \(~ 8Mio. gas for Görli Testnet\). 

#### Registering a new Template via the `Template` class from an ACTUS terms object

```typescript
const template = await Template.create(ap, TERMS);

// obtaining the registered TemplateTerms and TemplateSchedules
const templateTerms = await template.getTemplateTerms();
const templateSchedules = await template.getTemplateSchedules();
```

### Registered Templates on Görli Testnet

| TemplateId | Template Description |
| :--- | :--- |
| 0x84ef200c6c8acd8caac299d38d41b39ac8f863837f1d3f8bf7e9de7eef750117 | Buyer 3M-Amortizing Loan |
| 0x51f25b95a07d775a7d09751016b8d913b158d2c8687dfdf8ee44c7b3ac32ed24 | Buyer 12M-Bond |
| 0x9fd2391af29ad6ee431d9f36cd5e7204027b27e9d138719a6110763769abc8ff | Seller 2W-Bond |
| [view additional templates...](https://github.com/atpar/ap-monorepo/tree/master/packages/ap-contracts/templates/goerli) |  |

