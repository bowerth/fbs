---
layout: curriculum
title:  Input Data Sources
byline: Reference to input data sources used by the statistical modules
---

## Input and Output Location

Several modules that are taking information from agriculture:aproduction are saving results back to the agriculture:aproduction database after imputation.

However:

- output from the trade module is saved back to the trade domain
- tourism module is saving back to the tourism domain
- there are unused domains "food" and "industrial"

![data-input-imputation-output-location]({{ site.baseurl }}/assets/diagram/data-input-imputation-output-location.svg)

## Input Requirement Validation

![faoswsModules-ensure-main]({{ site.baseurl }}/assets/diagram/faoswsModules-ensure-main.svg)

## Keyword Search

### DatasetKey

- search R functions in `/R` folder for "DatasetKey"
- parse code block
- extract "domain" and "dataset"

{% include dryworkflow/dataset-depends-R.md %}

### DatasetKey

- search `main.R` scripts in `/modules` folder for "ReadDatatable"
- print code block

{% include dryworkflow/datatable-depends-R.md %}

## Extract from DESCRIPTION file

### swsDatasetDepends section

List of datasets used by module as mentioned in the DESCRIPTION file of each repository

{% include dryworkflow/dataset-depends-description.md %}

### Example for the `faoswsStandardization` Module

- [https://github.com/SWS-Methodology/faoswsStandardization/blob/master/DESCRIPTION](https://github.com/SWS-Methodology/faoswsStandardization/blob/master/DESCRIPTION)

```
swsDatasetDepends: 
    agriculture:aproduction,
    trade:total_trade_CPC,
    tourism:tourismprod,
    suafbs:sua,
    faostat_one:FS1_SUA,
    faostat_one:aupus_share_fs,
    faostat_one:input_from_proc_fs,
    SWS_R_SHARE/browning/elementCodes.csv
```

## Service at hqlqasws1.hq.un.fao.org:8080

### SWS Dataset Configuration

- [http://hqlqasws1.hq.un.fao.org:8080/dataset_configuration.html](http://hqlqasws1.hq.un.fao.org:8080/dataset_configuration.html)
- [FAO Statistical Standards - Metadata Annex 5 - Observation Status Codes](https://workspace.fao.org/tc/sws/userspace/_layouts/15/WopiFrame2.aspx?sourcedoc=/tc/sws/userspace/Shared%20Documents/Standards/SWS-05%20Annex-05%20Observation%20Status%20Codes.doc&action=default)

![hqlqasws1-dataset-description]({{ site.baseurl }}/assets/img/hqlqasws1-dataset-description.png)

### SWS Datatable Configuration

- at present, no service is available to provide metadata for datatable objects in the SWS. 
- using the R API and the `faosws` package, the `FetchDatatableConfig` function can retrieve the data types of columns
- these types do not necessarily correspond to the PostgreSQL standards
- see [8.1 Numeric Types](https://www.postgresql.org/docs/current/static/datatype-numeric.html) and [8.3. Character Types](https://www.postgresql.org/docs/current/static/datatype-character.html) for possible PostgreSQL data types
- `decimal` and `smalltext` in the following example are not mentioned

```
metadata <- faosws::FetchDatatableConfig(table = "ce_combinednomenclature_unlogged_2009")
metadata$ce_combinednomenclature_unlogged_2009$columns$sup_quantity$type
[1] "decimal"
metadata$ce_combinednomenclature_unlogged_2009$columns$period$type
[1] "smalltext"
```

### PostgreSQL Datatypes

Table 8-2. Numeric Types and Table 8-4. Character Types

| Name | Storage Size | Description | Range |
| ---- | ------------ | ----------- | ----- |
| decimal | variable | user-specified precision, exact |	up to 131072 digits before the decimal point; up to 16383 digits after the decimal point |
| character varying(n), varchar(n) | | variable-length with limit | |
| character(n), char(n) | | fixed-length, blank padded | |
| text | | variable unlimited length | |

## SWS Dataset Dimension Members

The tables below contain the list of unique members for selected dimensions. Only the first 10 entries are shown.

{% include dryworkflow/domain-dataset/domain-dataset-all.md %}

## SWS Datatables

Only the first 10 entries of each table are shown.

{% include dryworkflow/datatable/datatable-all.md %}

## SWS Rdata

Only the first 10 entries of each table are shown.

{% include dryworkflow/sws-rdata/sws-rdata-all.md %}

## Omitted Variables

### UNSD Comtrade HS Commodity Classification

{% include rmarkdown_fragment/faoswsTrade/fragment_spark_count_ct_tl_hsrep_csv.html %}

### Eurostat CN8 Stat Regime

{% include rmarkdown_fragment/faoswsTrade/fragment_spark_count_statregime_csv.html %}

## Commodity Classification Conversion

{% include rmarkdown_fragment/faoswsTrade/fragment_hsfclmap2_rds.html %}

## Eurostat

<!-- - [ext_esms metadata](http://ec.europa.eu/eurostat/cache/metadata/en/ext_esms.htm) -->

### Comext

#### Information from comextsupport@ec.europa.eu

- figures for VALUES sent by the Member States must not exceed 17 digits, that is 14 + 3 decimals
- for QUANTITY and SUP.QUANTITY it is 14 + 0 (no decimals)
- as we sometimes publish in 1000_EUR or 1000 KG (depending on the dataset), 3 decimals must always be foreseen

> in the SWS, the following data types are used: `value_1k_euro` numeric(20,2) `qty_ton` numeric(20,2) `sup_quantity` numeric(20,2) (see message 03 August 2016 11:16)

#### Format of Comext Data Files

- see [readme.txt](http://ec.europa.eu/eurostat/estat-navtree-portlet-prod/BulkDownloadListing?sort=1&file=comext%2Freadme.txt)

- format of data files: declarant country, partner country, product code, flow, statistical procedure, period, 
value in 1000ECU, value in tonnes, value in supplementary unit
- Each file corresponds to a period, ex : `nc200101.dat` --> January 2001

`FLOW`
:   `=1` for import `=2` for export

Product Code (`PRODUCT`)
:   CN8 (8 digits)  
    HS2 (2 digits)  
    (`TOTAL` code is "total trade")

Partner Country (`PARTNER`)
:   4 digits code

Statistical Procedure (`STAT_REGIME`)
:   1 digit code  
    statistical procedure 1 has to be calculated thanks to others: `RS1 = RS4-RS2-RS3-RS5-RS6-RS7-RS9`

- Regime 1: NORMAL IMPORTS of goods for final use in the EU
- Regime 2: NOT EXSISTING
- Regime 3: OUTWARD PROCESSING. Outward processing makes it possible to export goods
temporarily for processing and to import the transformed products, the added value of which will be subject to a full or partial exemption from duties and levies
- Regime 4: TOTAL IMPORTS. Sum of imports under the 5 statistical regimes
- Regime 5: INWARD PROCESSING: Imports that are to be re-exported as final goods, while benefiting from an exemption from duties or levies via a suspension or a reimbursement/drawback
- Regime 6: INWARD PROCESSING: Imports that are to be re-exported as final goods, while benefiting from an exemption from duties or levies via a suspension which would be carried out under the normally applicable trade policy
- Regime 7: ECONOMIC (outward) process arrangements for textiles

Declarant Country (`DECLARANT`)
:   3 digits code (`EU` is Europe)

Example of a `*.dat` file

```
DECLARANT,PARTNER,PRODUCT_NC,FLOW,STAT_REGIME,PERIOD,VALUE_1000ECU,QUANTITY_TON,SUP_QUANTITY
001,0003,01,1,4,200201,6191.13,1947.9,00
001,0003,01011010,1,4,200201,20.66,2.3,6
```

To get a `PRODUCT_NC` code of 4 or 6 digits, 8 digits corresponding codes have to be added. For example, code 1234 is the sum of all 8 digits codes beginning by 1234 (1234 = sum(1234????))

#### Nota Bene

- [Nota Bene for the indicators](http://epp.eurostat.ec.europa.eu/newxtweb/downloadobject.do?keepsessionkey=true&filenameOut=NB_Indicators.doc&mimeType=application/doc&objectID=507840560&objectType=LOB&disposition=attachment) (25088 Bytes) - Last updated date: 2010-01-19 

Data are disseminated according to the Combined Nomenclature (CN8 level) for the following indicators:

- trade value (in Euro),
- trade quantity in 100 kg,
- trade quantity in supplementary units (published in the Official Journal of the European Communities relating to the annual revision of the Combined Nomenclature

Value
:   Before legal existence of the Euro, values were calculated in ECU's. In all cases the average rates were used. 

Quantity
:   Data are rounded to 100 kg units. Therefore some very low figures or aggregations may have been influenced.

Supplementary Units
:   Supplementary units are the units measuring quantity, other than net mass expressed in kilograms. In the Combined Nomenclature you can find all the supplementary units for different commodities – such as number of items, number of m2, m3, pairs, dozens, etc. This is done because, for some products, it is necessary to indicate (in addition to the net mass) a supplementary unit in order to define the quantity or volume of the product. 
The supplementary units are published in the Official Journal for the Combined Nomenclature (CN). 

- see 2015/C 076/01 "Explanatory notes to the Combined Nomenclature of the European Union" in [Official Journal of the European Union C 76](http://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=OJ:C:2015:076:FULL&from=EN)

### Bulk Download

Lines 5642-5647 from [table_of_contents_en.txt](http://ec.europa.eu/eurostat/estat-navtree-portlet-prod/BulkDownloadListing?sort=1&file=table_of_contents_en.txt) at [Eurostat Bulk Download Listing](http://ec.europa.eu/eurostat/estat-navtree-portlet-prod/BulkDownloadListing) (access date: 2016-07-27)

{% include dryworkflow/eurostat-table-of-contents-en.md %}

##  UNSD Comtrade Tariffline

- data availability by reporter country and commodity classification [UN comtrade: daReportersResults.aspx](http://comtrade.un.org/db/mr/daReportersResults.aspx)
- data availability by year: [1990-1999, HS0-HS3](http://comtrade.un.org/db/mr/daYearsResults.aspx?y=1990,1991,1992,1993,1994,1995,1996,1997,1998,1999&px=H0,H1,H2,H3)
- REST SDMX 2.1 JSON API documentation [The UN Comtrade data extraction API](http://comtrade.un.org/data/doc/api/)

### HS Harmonized System

- if data was originally submitted to UN Comtrade in HS1996 then HS1996 is displayed
- `H0` HS 1992
- `H1` HS 1996
- `H2` HS 2002
- `H3` HS 2007
- `H4` HS 2012

### Data Access

#### Tariff Line (getSdmxTariffLineV1.aspx)

- link [http://comtrade.un.org/ws/getsdmxtarifflinev1.aspx?comp=false](http://comtrade.un.org/ws/getsdmxtarifflinev1.aspx?comp=false) will download "TariffLineSdmx.xml" (1016 MB)

#### Example Query (Tariffline)

- [http://comtrade.un.org/ws/getsdmxtarifflinev1.aspx?px=H2&y=2005&r=400&rg=1&p=392&cc=442190900&comp=false](http://comtrade.un.org/ws/getsdmxtarifflinev1.aspx?px=H2&y=2005&r=400&rg=1&p=392&cc=442190900&comp=false)

- `px`: `H2`  (Group: CL: `HS 2002`)
- `y`: `2005` (Group: time)
- `r`: `400` (Group: RPT: `Jordan`)
- `rg`: `1` (Section: TF: `imports`)
- `p`: `392` (Obs: PRT: `Japan`)
- `cc`: `442190900` (Obs: CC-H2: `Articles of Wood (Other)`) [hscode.cfm?code=4421](http://www.foreign-trade.com/reference/hscode.cfm?code=4421)

#### Dimensions

- `px`: commodity classification
- `y`: year
- `r`: reporter country
- `rg`: trade flow
- `p`: partner country
- `cc`: commodity code
- `comp`: compress
- `count`

![Table: UN Comtrade Web Services Access Points and its Parameters](http://unstats.un.org/unsd/tradekb/Uploads/Images/AccessPoint.jpg)

#### Metadata and data availability

- Commodity List URL example: get 2 digit HS1996 [refs/getCommodityList.aspx?px=H1&cc=??](http://comtrade.un.org/ws/refs/getCommodityList.aspx?px=H1&cc=??)
- Country List URL example: get all country codes [refs/getCountryList.aspx](http://comtrade.un.org/ws/refs/getCountryList.aspx)
- Explanatory Notes [refs/getExplanatoryNotes.aspx](http://comtrade.un.org/ws/refs/getExplanatoryNotes.aspx)
- Data Availability [refs/getDataAvailablity.aspx](http://comtrade.un.org/ws/refs/getDataAvailablity.aspx)

#### Description of Tariff Line Product Code by Country

World Bank have done some work to identify the Tariff line product code description using a combination of WTO IDB, UNCTAD TRAINS and HS 6 digit level product description for the UN COMTRADE tariff line data.

The file can be downloaded from [http://wits.worldbank.org/data/public/CMTTL_TarifflineDescription.zip](http://wits.worldbank.org/data/public/CMTTL_TarifflineDescription.zip) (137 MB)

#### TariffLine XML file structure

```
<?xml version="1.0" encoding="utf-8"?>
  <CrossSectionalData xmlns="http://www.SDMX.org/resources/SDMXML/schemas/v1_0/message" xmlns:uncs="http://unstats.un.org/structure/key_families/cross/UN_COMTRADE_H2" xmlns:cross="http://www.SDMX.org/resources/SDMXML/schemas/v1_0/cross" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:schemaLocation="http://www.SDMX.org/resources/SDMXML/schemas/v1_0/message SDMXMessage.xsd http://unstats.un.org/structure/key_families/cross/UN_COMTRADE_H2 UN_COMTRADE_H2_CrossSectional.xsd http://www.SDMX.org/resources/SDMXML/schemas/v1_0/cross SDMXCrossSectionalData.xsd">
  <Header>
    <ID>UN1105460460</ID>
    <Test>true</Test>
    <Truncated>false</Truncated>
    <Prepared>2016-09-22T12:25:12</Prepared>
    <Sender id="UN"><Name xml:lang="en">United Nations</Name></Sender>
    <KeyFamilyRef>UN_COMTRADE_H2</KeyFamilyRef>
    <DataSetID>01</DataSetID>
    <DataSetAction>Update</DataSetAction>
    <Extracted>2016-09-22T12:25:12</Extracted>
  </Header>
    <uncs:DataSet>
      <uncs:Group RPT="400" time="2005" CL="H2" UNIT_MULT="1" DECIMALS="1" CURRENCY="USD" FREQ="A" TIME_FORMAT="P1Y" REPORTED_CLASSIFICATION="H2" FLOWS_IN_DATASET="MXR">
        <uncs:Section TF="1" REPORTED_CURRENCY="JOD" CONVERSION_FACTOR="1.410440" VALUATION="CIF" TRADE_SYSTEM="Special" PARTNER="Origin">
          <uncs:Obs CC-H2="442190900" PRT="392" netweight="438" qty="438" QU="8" value="2238.36828" EST="0" HT="0" />
          <uncs:Obs CC-H2="442190900" PRT="422" netweight="88883" qty="88883" QU="8" value="385604.42292" EST="0" HT="0" />
          ...
          </uncs:Section>
        </uncs:Group>
    </uncs:DataSet>
</xml>
```

#### Read using rsdmx package

```
> as.data.frame(readSDMX("http://comtrade.un.org/ws/getsdmxtarifflinev1.aspx?px=H2&y=2005&r=400&rg=1&p=392&cc=442190900&comp=false"))
RPT time CL UNIT_MULT DECIMALS CURRENCY FREQ TIME_FORMAT
1 400 2005 H2         1        1      USD    A         P1Y
  REPORTED_CLASSIFICATION FLOWS_IN_DATASET TF REPORTED_CURRENCY
1                      H2              MXR  1               JOD
  CONVERSION_FACTOR VALUATION TRADE_SYSTEM PARTNER obs     CC.H2 PRT netweight
1          1.410440       CIF      Special  Origin Obs 442190900 392       438
  qty QU      value EST HT
1 438  8 2238.36828   0  0

```

|RPT |time |CL |UNIT_MULT |DECIMALS |CURRENCY |FREQ |TIME_FORMAT |REPORTED_CLASSIFICATION |FLOWS_IN_DATASET |
|:---|:----|:--|:---------|:--------|:--------|:----|:-----------|:-----------------------|:----------------|
|400 |2005 |H2 |1         |1        |USD      |A    |P1Y         |H2                      |MXR              |

|TF |REPORTED_CURRENCY |CONVERSION_FACTOR |VALUATION |TRADE_SYSTEM |PARTNER |obs |CC.H2     |PRT |
|:--|:-----------------|:-----------------|:---------|:------------|:-------|:---|:---------|:---|
|1  |JOD               |1.410440          |CIF       |Special      |Origin  |Obs |442190900 |392 |

|netweight |qty |QU |value      |EST |HT |
|:---------|:---|:--|:----------|:---|:--|
|438       |438 |8  |2238.36828 |0   |0  |
