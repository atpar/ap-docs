# Templates

Assets have to be based on an already registered template \(see list of registered Templates on Görli Testnet below\). 

A template is comprises a set of `TemplateTerms` \(see. ...\) and `TemplateSchedules`. `TemplateSchedules` are a set of event type specific arrays containing raw events with relative timestamp \(or offsets\). In the `CustomTerms` of the asset the `anchor date` attribute is used to calculate the actual schedule time.

Anyone is able to register new  templates. `ap.js` provides methods for generating  `TemplateTerms` and `TemplateSchedules`from an ACTUS terms object.  

#### Deriving `TemplateTerms` and `TemplateSchedules` and  from an ACTUS terms object

```typescript
const templateTerms = ap.utils.convert.toTemplateTerms(TERMS);

// provide the corresponding ACTUS Engine and the ACTUS terms object
const templateSchedules = await ap.utils.schedule.generateTemplateSchedules(
  ap.contracts.engine(ENGINE_ADDRESS),
  TERMS
);
```

#### Registering a new template

The number of events for `TemplateSchedules` is bound by the block gas limit \(~ 8Mio. gas for Görli Testnet\). 

```typescript
const tx = await ap.contracts.templateRegistry.methods.registerTemplate(
  templateTerms,
  templateSchedules
).send({ from: ACCOUNT });

// retrieve the id of the template from the event logs
const { templateId } = tx.events.RegisteredTemplate.returnValues;
```

### Registered Template

| TemplateId | Template Description |
| :--- | :--- |
|  |  |

