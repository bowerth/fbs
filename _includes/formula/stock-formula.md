
Model based on historical changes
URL
:   file://///HQFILE4/ESS_admin/ESS/Team_working_folder/A/FBS-Methods/OrangeBook/book/6_stocks/Stocks_master.docx

Label
:   Equations 9, 10

- delta stock changes `\Delta \mathsf{S}\_{t-i}` (&#916S;)
- time `t`
- numebr of previous stock changes `k`
- error term `\epsilon_(t)` (&#949;)

\\[ \Delta \mathsf{S}\_{t} = \beta \left( \sum\limits_{i=1}^{k} \Delta \mathsf{S}\_{t-i} \right) + \epsilon\_{t}\  \\]

 We could alternatively express this as
 
\\[ \Delta \mathsf{S}\_{t} \sim N \left( \beta \sum\limits_{i=1}^{k} \Delta \mathsf{S}\_{t-i} , \sigma^{2} \right) \\]

### R `lm` Implementation

The current implementation of the module is different from the Orange Book. The module is using only delta production. The formula currently included in the Orange Book may need to be subject to revision.

```{r}
  stocksModel <- lm(deltaStocks ~ deltaProduction, 
          data = newSuaData[deltaProduction != 0 & 
                              deltaStocks != 0])
```
