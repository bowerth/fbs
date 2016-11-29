
## Conversion Key fcl_2_cpc

|fcl       |cpc       |
|:---------|:---------|
|smalltext |smalltext |

{% include dryworkflow/datatable/Conversion-Key-fcl_2_cpc.md %}

## Conversion Key hsfclmap2

|validyear |area    |flow    |fromcode  |tocode    |fcl     |mdbyear |mdbarea   |mdbfcl    |
|:---------|:-------|:-------|:---------|:---------|:-------|:-------|:---------|:---------|
|integer   |integer |integer |smalltext |smalltext |integer |integer |smalltext |smalltext |

{% include dryworkflow/datatable/Conversion-Key-hsfclmap2.md %}

## Data Table ce_combinednomenclature_unlogged_2009

|chapter   |declarant |partner   |product_nc |flow      |stat_regime |period    |value_1k_euro |qty_ton |sup_quantity |
|:---------|:---------|:---------|:----------|:---------|:-----------|:---------|:-------------|:-------|:------------|
|smalltext |smalltext |smalltext |smalltext  |smalltext |smalltext   |smalltext |decimal       |decimal |decimal      |

{% include dryworkflow/datatable/Data-Table-ce_combinednomenclature_unlogged_2009.md %}

## Data Table ct_tariffline_unlogged_2009

|chapter   |rep       |tyear     |curr      |hsrep     |flow      |repcurr   |comm      |prt       |weight  |qty     |qunit     |tvalue  |est       |ht        |
|:---------|:---------|:---------|:---------|:---------|:---------|:---------|:---------|:---------|:-------|:-------|:---------|:-------|:---------|:---------|
|smalltext |smalltext |smalltext |smalltext |smalltext |smalltext |smalltext |smalltext |smalltext |decimal |decimal |smalltext |decimal |smalltext |smalltext |

{% include dryworkflow/datatable/Data-Table-ct_tariffline_unlogged_2009.md %}

## Imputation Key fbs_production_comm_codes

|fbs_domain |fbs_dataset |fbs_key |fbs_code |
|:----------|:-----------|:-------|:--------|
|text       |text        |text    |text     |

{% include dryworkflow/datatable/Imputation-Key-fbs_production_comm_codes.md %}
