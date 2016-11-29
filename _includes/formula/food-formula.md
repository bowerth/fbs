
### Log-log function

- country $i$
- commodity $j$
- trendfactor $\phi_{i}$
- income elasticity of demand $\epsilon_{ij}$

Per-capita Food Consumption:

\\[ \mathsf{FoodPC}\_{t,ij} = \mathsf{FoodPC}\_{t-1,ij} + e^{\epsilon\_{ij} \log \left( \Delta \mathsf{Y}\_{t,i} \right) }  + \phi\_{i} * \mathsf{FoodPC}\_{t-1,ij} \\]

<!-- \\[ \frac{ \mathsf{Food}\_{t,ij} }{ \mathsf{Pop}\_{t,i} } = \frac{ \mathsf{Food}\_{t-1,ij} }{ \mathsf{Pop}\_{t-1,i} } + \exp \left( \epsilon\_{ij} \log \left( \Delta \mathsf{Y}\_{t,i} \right) \right) + \phi\_{i} * \frac{ \mathsf{Food}\_{t-1,ij} }{ \mathsf{Pop}\_{t-1,i} } \\] -->

<!-- with **trendfactor** `\phi_(i)=0` -->

This corresponds to

\\[ \mathsf{FoodPC}\_{t,ij} =  \left( 1 + \phi\_{i} \right) \mathsf{FoodPC}\_{t,ij} + e^{\epsilon\_{ij} \log \left( \Delta \mathsf{Y}\_{t,i} \right) } \\]

expanding per-capita food consumption

\\[ \mathsf{FoodPC}\_{t,ij} = \frac{ \mathsf{Food}\_{t,ij} }{ \mathsf{Pop}\_{t,i} } \\]

\\[ \frac{ \mathsf{Food}\_{t,ij} }{ \mathsf{Pop}\_{t,i} } = \left( 1 + \phi\_{i} \right) \frac{ \mathsf{Food}\_{t-1,ij} }{ \mathsf{Pop}\_{t-1,i} } + e^{\epsilon\_{ij} \log \left( \Delta \mathsf{Y}\_{t,i} \right) } \\]

multiply both sides with $Pop_{t, ij}$

\\[ \mathsf{Food}\_{t,ij} = \mathsf{Pop}\_{t,i} * \left[ \left( 1 + \phi\_{i} \right) \frac{ \mathsf{Food}\_{t-1,ij} }{ \mathsf{Pop}\_{t-1,i} } + e^{\epsilon\_{ij} \log \left( \Delta \mathsf{Y}\_{t,i} \right) } \right] \\]

\\[ \mathsf{Food}\_{t,ij} = \frac{ \mathsf{Pop}\_{t,i} }{ \mathsf{Pop}\_{t-1,i} } * \left( 1 + \phi\_{i} \right) \mathsf{Food}\_{t-1,ij} + \mathsf{Pop}\_{t,i} * e^{\epsilon\_{ij} \log \left( \Delta \mathsf{Y}\_{t,i} \right) } \\]

with

\\[ \Delta \mathsf{Pop}\_{t,i} = \frac{ \mathsf{Pop}\_{t,i} }{ \mathsf{Pop}\_{t-1,i} } \\]

it becomes

\\[ \mathsf{Food}\_{t,ij} = \Delta \mathsf{Pop}\_{t,i} * \left( 1 + \phi\_{i} \right) \mathsf{Food}\_{t-1,ij} + \mathsf{Pop}\_{t,i} * e^{\epsilon\_{ij} \log \left( \Delta \mathsf{Y}\_{t,i} \right) } \\]

where $\Delta Y_{t,i}$ is the per-capita GDP change

\\[ \Delta \mathsf{Y}\_{t,i} = \frac{ \mathsf{GDPPC}\_{t,i} }{ \mathsf{GDPPC}\_{t-1,i} } \\]

###Linear function

Per-capita Food Consumption:
\\[ \mathsf{FoodPC}\_{t,ij} = \mathsf{FoodPC}\_{t-1,ij} + \phi\_{i} * \mathsf{FoodPC}\_{t-1,ij} \\]

This corresponds to

\\[ \frac{ \mathsf{Food}\_{t,ij} }{ \mathsf{Pop}\_{t,i} } = \left( 1 + \phi\_{i} \right) \frac{ \mathsf{Food}\_{t-1,ij} }{ \mathsf{Pop}\_{t-1,i} } \\]

multiply both sides with $Pop_{t, ij}$

\\[ \mathsf{Food}\_{t,ij} = \mathsf{Pop}\_{t,i} * \left[ \left( 1 + \phi\_{i} \right) \frac{ \mathsf{Food}\_{t-1,ij} }{ \mathsf{Pop}\_{t-1,i} } \right] \\]


\\[ \mathsf{Food}\_{t,ij} = \frac{ \mathsf{Pop}\_{t,i} }{ \mathsf{Pop}\_{t-1,i} }  *  \left( 1 + \phi\_{i} \right) { \mathsf{Food}\_{t-1,ij} }  \\]

\\[ \mathsf{Food}\_{t,ij} = \Delta \mathsf{Pop}\_{t,i} * \left( 1 + \phi\_{i} \right) \mathsf{Food}\_{t-1,ij}  \\]

### Semi-log function

Per-capita Food Consumption:

\\[ \mathsf{FoodPC}\_{t,ij} = \mathsf{FoodPC}\_{t-1,ij}  * \left[1 + \epsilon\_{ij} \log \left( \Delta \mathsf{Y}\_{t,i} \right) \right]+ \phi\_{i} * \mathsf{FoodPC}\_{t-1,ij}  \\] 

\\[ \mathsf{FoodPC}\_{t,ij} =  \mathsf{FoodPC}\_{t-1,ij} *  \left[1 + \epsilon\_{ij} \log \left( \Delta \mathsf{Y}\_{t,i} \right) + \phi\_{i} \right]  \\]

\\[ \frac{ \mathsf{Food}\_{t,ij} }{ \mathsf{Pop}\_{t,i} } =  \frac{ \mathsf{Food}\_{t-1,ij} }{ \mathsf{Pop}\_{t-1,i} }   *  \left[1 + \epsilon\_{ij} \log \left( \Delta \mathsf{Y}\_{t,i}\right) + \phi\_{i} \right]  \\]

multiply both sides with $Pop_{t, ij}$

\\[\mathsf{Food}\_{t,ij} =  \frac{ \mathsf{Pop}\_{t,i} }{ \mathsf{Pop}\_{t-1,i} } * \mathsf{Food}\_{t-1,ij}  * \left[1 + \epsilon\_{ij} \log \left( \Delta \mathsf{Y}\_{t,i} \right) + \phi\_{i}\right]  \\]

\\[ \mathsf{Food}\_{t,ij}  =  \Delta \mathsf{Pop}\_{t,i} * \mathsf{Food}\_{t-1,ij} * \left[1 + \epsilon\_{ij} \log \left( \Delta \mathsf{Y}\_{t,i}\right) + \phi\_{i}\right]  \\]

### Log-inverse function

Per-capita Food Consumption:

\\[ \mathsf{FoodPC}\_{t,ij} = \mathsf{FoodPC}\_{t-1,ij} * e^{\epsilon\_{ij} \left( 1 - \frac{ \mathsf{1}}{ \Delta \mathsf{Y}\_{t,i} } \right)} + \phi\_{i} * \mathsf{FoodPC}\_{t-1,ij} \\]

\\[ \mathsf{FoodPC}\_{t,ij} = \mathsf{FoodPC}\_{t-1,ij} * \left[  e^{\epsilon\_{ij} \left( 1 - \frac{ \mathsf{1}}{ \Delta \mathsf{Y}\_{t,i} } \right)} +  \phi\_{i}\right] \\]

\\[ \frac{ \mathsf{Food}\_{t,ij} }{ \mathsf{Pop}\_{t,i} } =  \frac{ \mathsf{Food}\_{t-1,ij} }{ \mathsf{Pop}\_{t-1,i} }   * \left[  e^{\epsilon\_{ij} \left( 1 - \frac{ \mathsf{1}}{ \Delta \mathsf{Y}\_{t,i} } \right)} +  \phi\_{i}\right] \\]

multiply both sides with $Pop_{t, ij}$

\\[\mathsf{Food}\_{t,ij} =  \frac{ \mathsf{Pop}\_{t,i} }{ \mathsf{Pop}\_{t-1,i} } * \mathsf{Food}\_{t-1,ij} * \left[ e^{\epsilon\_{ij} \left( 1 - \frac{ \mathsf{1}}{ \Delta \mathsf{Y}\_{t,i} } \right)} +  \phi\_{i} \right] \\]

\\[ \mathsf{Food}\_{t,ij} = \Delta \mathsf{Pop}\_{t,i} * \mathsf{Food}\_{t-1,ij}   * \left[ e^{\epsilon\_{ij} \left( 1 - \frac{ \mathsf{1}}{ \Delta \mathsf{Y}\_{t,i} } \right)} +  \phi\_{i} \right] \\]

<!--\left( \exp \left( \epsilon\_{ij} \left( 1 - \frac{ \mathsf{1}}{ \Delta \mathsf{Y}\_{t,i} } \right) \right) + \phi\_{i} \right) -->
<!--\\[ e^{} \\]-->

