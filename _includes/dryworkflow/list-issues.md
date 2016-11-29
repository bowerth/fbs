### faoswsFeed



### faoswsFood



### faoswsIndustrial



### faoswsLoss



### faoswsProduction



### faoswsSeed



### faoswsStandardization

**[Add intermediate save to balanceResidual](https://github.com/SWS-Methodology/faoswsStandardization/issues/23)**

- When module compiles unbalanced SUA, it should create an element which is the availability in the crude balancing step. This can be done as a SaveData call in balanceResidual. Probably to the sua table?

**[Incomplete extraction rates and shares](https://github.com/SWS-Methodology/faoswsStandardization/issues/22)**

- I'm fairly sure that these tables are incomplete. They come from the `aupus_ratio` table - I need to check their status.

**[Nutritive factors seem missing](https://github.com/SWS-Methodology/faoswsStandardization/issues/3)**

- We currently have no calorie/protein/fat factors for wheat flour (across all countries and all years).  Clearly we must be missing some data...

**[Specify food/feed/industrial/... commodities](https://github.com/SWS-Methodology/faoswsStandardization/issues/1)**

- In the standardization process, the balanceResidual function will balance the SUA level commodities by assigning imbalances to a specific variable.  For example, if the balance for flour has an excess of 5,000 tons, this amount will be added to the food of flour (while for bran it would be allocated to feed).  We need to implement the list specifying what variable certain commodities get allocated to (food, feed, industrial uses, etc.) and incorporate this information into the balanceResidual function.

### faoswsStock



### faoswsTourist



### faoswsTrade

**[EU Commission - Combined Nomenclature table for 1999-2008](https://github.com/SWS-Methodology/faoswsTrade/issues/33)**

- Currently, the Datatables don't seem to be on the working system.

**[Key not found for dimension measuredItemCPC](https://github.com/SWS-Methodology/faoswsTrade/issues/26)**

- There are a number of CPC codes that aren't in the destination table for Total trade. I'm not sure as to why that is, but among them are `01241.90`, `01919.96` and `21419.91`.

