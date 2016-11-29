<!-- included in faq/index.md -->

### 2016-08-31 Educate country-level FBS compilers

#### Who can access the UNWTO Elibrary ? 

The Elibrary has special conditions for our Member States’ governmental institutions. See http://www.e-unwto.org/subscribe.

Other institutions can purchase admission to the commercial interface of the Elibrary by yearly subscription. The commercial level of the Elibrary does not, however, include restricted or privileged information.  See http://www.e-unwto.org/pb-assets/unwto/Rules_MS_en.pdf.

#### What is the time period of "historic amount of daily nutrients consumed"?

At present, the module only uses information from the current period

```
foodConsumptionPopData.3[, calPerPersonPerDay := (totalFood * valueCal * calUnit) / daysperyear / (pop * popUnit)]
```

where

- `totalFood` is the amount of food available (in tons, from food module)
- `valueCal`  is the caloric content (for each commodity)
- `calUnit` is 10000
- `daysperyear` is 365
- `pop` is the total population (in thousand persons, for each country)
- `popUnit` is 1000

#### At what step is the number of nutrients converted back to amount of food?

```
foodTouristConsumption.11[, netFood := calNetCountry/(valueCal * calUnit)]
```

where

- `calNetCountry` is the net tourist calories per country
- `valueCal` is the caloric content (for each commodity)
- `calUnit` is 10000
 
#### Which dietary pattern do tourists follow abroad? Do we assume that tourists consume the same amount (level) of calories abroad as they consume in their respective country of origin?

In our approach, the person comes from country A to country B eats the same food types as people in country B but eats the same calorie amounts as in their home country. In case we don't have totalCalDay for the country A, we will assume the same calories amount in country B. See https://github.com/SWS-Methodology/faoswsTourist/blob/master/modules/impute_tourist/main.R#L228.

