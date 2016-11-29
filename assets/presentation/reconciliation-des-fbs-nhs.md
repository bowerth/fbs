
Reconciliation between dietary energy consumption from FBS and NHS
=

### Dietary Energy Supply

Dietary Energy Supply (DES) refers to food available for human consumption during the course of the reference period, expressed in terms of energy (kcal/person/day).

#### Reasons for using consumption estimates from Food Balance Sheets

- covers practically all countries of the world
- regularly revised and up-dated
- readily available source of information for the PoU at the national level
- assess impact on the distribution of dietary energy consumption
- assess combined effect of food supply increase and inequality reduction

---

### FBS Scope

Covers value chain from Post-Harvest to Retail (Pre-Harvest and Retail sales are not covered)

```flow
st=>start: Pre-Harvest
op1=>operation: Post-Harvest
op2=>operation: Farm
op3=>operation: Processing
op4=>operation: Export
op5=>operation: Wholesale
e=>end: Retail

st->op1->op2->op3->op4->op5->e
```

---

### NHS Scope

Only covers household consumption (Retail and Individual level are not covered, neither non-household)

```flow
st=>start: Retail
op=>operation: Household
e=>end: Individual

st->op->e
```

---

## New FBS methods

### overall approach is the same: FBS are based on item level Supply Utilization Accounts

- Total supply = total utilization:

\\[ P + I - \Delta St = X + Fo + Fe + Lo + Se + IU + T + ROU \\]

- $ \Delta St = St_{t} - St_{t-1} $, $P$ = production, $I$ = imports, $X$ = exports, $St$ = stock level, $Fo$ = food, $Fe$ = feed, $Lo$ = losses and waste, $Se$ = seed, $IU$ = industrial use,  $T$ = tourist consumption, and $ROU$ = residual other use

- 600+ SUA's converted in 95 FBS equations through a standardization process using commodity trees to link processed food commodities in their primary equivalent

---

## New FBS methods

### limitations of the previous methodology 

- Many manual estimates of the less informed elements (stocks, losses, industrial use, tourism consumption)
- Food consumption obtained as a residual, thus absorbing the cumulated error in all other elements
- Standardization module had become a black box. Some operations were hard coded (standardizing vegetable fats in their primary oilcrop equivalent) leading to negative utilizations
- Balancing the SUA's was in many instances a manual operation, obtained by adjusting the various elements until the balance was obtained

---

## New FBS methods

### address these limitations  

- Reduce the cumulated error and have no unknown element in the SUA equation: 8 modules imputing missing data for each SUA element (production, trade, feed, seed, losses, stocks, industrial utilization, tourist consumption) based on statistical modeling or regression functions
- Food consumption estimated separately
- Standardization module has been untangled
- Balancing is obtained with a maximum likelihood approach 

---

### Food Module

Illustrate Food Module

- [food module diagram](http://hqlprsws1.hq.un.fao.org/fbsmodules/modules/#food-module)

### Balancing Module

- Maximum-Likelihood approach

---

## Points for discussion

- objective: improve food consumption estimates
- how can hh surveys be used to improve Food estimates in the FBS?
- how can hh surveys be used to validate the FBS?
- which suggested approaches were not followed in the past?
- what are the acceptable gaps between data sources (FBS, NHS)?
- what case studies (in addition to USA, e.g. Mexico?)

