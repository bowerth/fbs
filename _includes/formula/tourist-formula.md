
Model based on historical changes

URL
:   file://///HQFILE4/ESS_admin/ESS/Team_working_folder/A/FBS-Methods/OrangeBook/book/9_Tourists/Tourist%20Consumption_master.docx

Label
:   Equations 23, 24, 25

Calculate total number of tourist days `N\_{T}`

\\[ N\_{T} = N\_{D} + N\_{O} \bar{D} \\]

- number of day visitors `N\_{D}`
- number of overnight visitors `N\_{O}`
- information on the average number of nights stayed within each country `\bar{D}`

Change in amount of food availability for commodity `i` in country `j`

\\[ \Delta TC\_{ij} = - \sum\_{k = 1, k \ne j}^{m} N\_{jk} f\_{ij} + \sum\_{l = 1, l \ne j}^{m} N\_{lj} f\_{il} \\]

Suggested alternative notation:

\\[ Net TC\_{ij} = \sum\_{l = 1, l \ne j}^{m} N\_{lj} f\_{il} - \left( \sum\_{k = 1, k \ne j}^{m} N\_{jk} \right) * f\_{ij} \\]

- $N\_{lj}$ represents the number of tourists travelling from country $l$ to country $j$
- $f\_{il}$ represents the historic amount of daily nutritients consumed within commodity $i$ and in country $l$
- $k$ represents any third country
- $m$ represents the set of possible countries in which tourism can occur

This can be simplified to

\\[ \Delta TC\_{ij} = - N\_{T} f\_{ij} + \sum\_{l = 1, l \ne j}^{m} N\_{lj} f\_{il} \\]

### R module Implementation

The current implementation of the module is different from the Orange Book. [...]

```{r}
  touristModel <- lm(...)
```
