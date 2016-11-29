
### Hierarchical linear model (HLM)

URL
:   file://///HQFILE4/ESS_admin/ESS/Team_working_folder/A/FBS-Methods/OrangeBook/book/11_loss/Loss_master.docx

Label
:   Equation 27a-e

\\[ \log \left( \mathsf{Loss}\_{ijklm} \right) = \alpha\_{1} t + \alpha\_{2ijkl} \log \left( \mathsf{Production}\_{ijklm} + 1 \right) + \mathsf{A}\_{ijklm} \\]

\\[ \alpha\_{2ijkl} = \beta\_{20} + \beta\_{2ijk} \left( \mathsf{Country:Commodity} \right)\_{ijkl} + \mathsf{B}\_{ijkl} \\]

\\[ \beta\_{2ijk} = \gamma\_{20} + \gamma\_{2ij} \left( \mathsf{Commodity} \right) + \mathsf{C}\_ijk \\]

\\[ \gamma\_{2ij} = \delta\_{20} + \delta\_{2i} \left( \mathsf{Food Group} \right) + D\_{ij} \\]

\\[ \delta\_{2i} = \zeta\_{20} + \zeta\_{21} \left( \mathsf{Food Perishable Group}\_{i} \right) + \mathsf{E}\_{i} \\]

### R `lme4` Implementation

The current implementation of the module is different from the Orange Book. The module includes imports (measuredElementTrade_5610). The formula currently included in the Orange Book may need to be subject to revision.

```{r}
  lossLmeModel =
    lmer(log(Value_measuredElement_5016 + 1) ~
           -1 +
           timePointYears +
           log(Value_measuredElement_5510 + 1) + 
           (-1 + log(Value_measuredElement_5510 + 1)|
            foodPerishableGroup/foodGroupName/measuredItemCPC/geographicAreaM49)+
           log(Value_measuredElementTrade_5610 + 1) +
           (-1 + log(Value_measuredElementTrade_5610 + 1)|
            measuredItemCPC/geographicAreaM49),
         data = finalModelData)
```
