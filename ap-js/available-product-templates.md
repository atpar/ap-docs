# Products

Assets have to be based on an already registered product \(see list of registered Products on Görli Testnet below\). 

A product is comprises a set of `ProductTerms` \(see. ...\) and `ProductSchedules`. `ProductSchedules` are a set of event type specific arrays containing raw events with relative timestamp \(or offsets\). In the `CustomTerms` of the asset the `anchor date` attribute is used to calculate the actual schedule time.

Anyone is able to register new  products. `ap.js` provides methods for generating  `ProductTerms` and `ProductSchedules`from an ACTUS terms object.  

#### Deriving `ProductTerms` and `ProductSchedules` and  from an ACTUS terms object

```typescript
const productTerms = ap.utils.convert.toProductTerms(TERMS);

// provide the corresponding ACTUS Engine and the ACTUS terms object
const productSchedules = await ap.utils.schedule.generateProductSchedules(
  ap.contracts.engine(ENGINE_ADDRESS),
  TERMS
);
```

#### Registering a new product

The number of events of all `ProductSchedules` is bound by the block gas limit \(~ 8Mio. gas for Görli Testnet\). 

```typescript
const tx = await ap.contracts.productRegistry.methods.registerProduct(
  productTerms,
  productSchedules
).send({ from: ACCOUNT });

// retrieve the id of the product from the event logs
const { productId } = tx.events.RegisteredProduct.returnValues;
```

### Registered Products

| ProductId | Product Description |
| :--- | :--- |
|  |  |

