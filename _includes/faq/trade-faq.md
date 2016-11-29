<!-- included in faq/index.md -->

### 2016-11-10

- Some observations measured in monetary values have `I` as **observation status flag**? Aren't monetary values supposed to remain unchanged?

The `I` ObservationStatus flags are added to observations that are considered as "unit value outliers". An observation's unit value is calculated as the ratio between the monetary value and the quantity `value / qty`. The calculated ratio can be extreme due to either the nominator or the denominator. Therefore, the flag is added to both measures (monetary value and quantity).

In the mirror step, monetary values are modified to account for differences between higher **CIF** prices for imports compared to **FOB** prices for exports.


- Could we use `E` as **observation status flag** for records added in the **mirror trade** step?

"Estimated values" refers to observations obtained through an estimation methodology (e.g. to produce back-casts) or based on the use of a limited amount of data or ad hoc sampling and through additional calculations (e.g. to produce a value at an early stage of the production stage while not all data are available). It may also be used in case of experimental data (e.g. in the context of a pilot ahead of a full scale production process) or in case of data of (anticipated/assessed) low quality. If needed, additional (uncoded) information can be provided through (free text) "comments" at the observation level or at a higher level.

The "Mapping from old to proposed flags in FAOSTAT dissemination system" table mentions: `Estimated data using trading partners database (mirror data) R -> E`


- Could we use `M` as **observation status flag** for the quantity measure of FCL items that are categorized as `$ value only`? What is the appropriate **method flag**? If those quantitiesare not published, are `M` flags required for intenal use?

`M`	Missing value (data cannot exist, not applicable)
:   Used to denote empty cells resulting from the impossibility to collect a statistical value (e.g. a particular education level or type of institution may be not applicable to a given country's education system)


- Could we use `X` as **observation status flag** and `h` as **method flag** for all HS input data (all information is raw data published by Eurostat and UNSD)

`X` Figure from international organizations
:   Observations reported by governmental international organizations (e.g. UN, ILO, WB, UNESCO etc. specification on which international organization is provided in the metadata)  
   `h` Collected using automatic data harvesting

The document may need to be revised, the table mentions for `<blank>`: "Observation reported by official statistical government agencies, **including Eurostat**."


- At which step can address period-specific issues with the input data? For example, in year 2000 the partner country code for China `156` is confused with the partner country code for Belgium `56`.

Issues in kind should already be addressed in the database. Otherwise, it is impossible to join data with mapping tables before exporting to analytical and statistical tools.

### 2016-10-10

- Similar to Production, gives slightly different results on different runs. Not a random seed problem. Possibly floating point error.

This statement is based on a test where four sessions were started and in each of them the trade module has been executed with identical parameter settings (year: 2009, out\_coef: 1.5). The extraction from the [log file]({{ site.baseurl }}/assets/data/Rserve.log_2016-08-01-09-57-42) below shows that between 77.6% and 78% of HS codes in Eurostat do not get converted to FCL. In case of Comtrade the conversion however is stable at 31.5%.

The [messages](http://hqlprsws1.hq.un.fao.org/fbsmodules/performance/#4-processes-same-year) generated at the end of the four module runs show that each additional run appends less values to the dataset. The first run terminates at 17:17:35 and appends 7589 values (less than 0.6% of the dataset), the last run terminates at 17:22:02 and appends 3912 values (less than 0.3% of the dataset). The total dataset for one year has more than 1.4 mio observations.

```
[2016-07-25 15:54:00]  [20610] Convert Eurostat HS to FCL
[2016-07-25 15:54:25]  [20626] Convert Eurostat HS to FCL
[2016-07-25 15:54:31]  [20633] Convert Eurostat HS to FCL
[2016-07-25 15:54:46]  [20697] Convert Eurostat HS to FCL
[2016-07-25 16:13:48]  Proportion of HS-codes not converted in FCL: 77.6%
[2016-07-25 16:13:52]  Proportion of tradeflows with nonmapped HS-codes: 88.1%
[2016-07-25 16:13:52]  Share of value of tradeflows with nonmapped HS-codes in total value: 94.5%
[2016-07-25 16:13:55]  [20610] Converting from comtrade to FAO codes
[2016-07-25 16:14:40]  Proportion of HS-codes not converted in FCL: 77.9%
[2016-07-25 16:14:43]  Proportion of HS-codes not converted in FCL: 77.8%
[2016-07-25 16:14:45]  Proportion of tradeflows with nonmapped HS-codes: 88.2%
[2016-07-25 16:14:45]  Share of value of tradeflows with nonmapped HS-codes in total value: 94.4%
[2016-07-25 16:14:48]  [20633] Converting from comtrade to FAO codes
[2016-07-25 16:14:48]  Proportion of tradeflows with nonmapped HS-codes: 88.2%
[2016-07-25 16:14:48]  Share of value of tradeflows with nonmapped HS-codes in total value: 94.4%
[2016-07-25 16:14:48]  Proportion of HS-codes not converted in FCL: 78%
[2016-07-25 16:14:51]  [20626] Converting from comtrade to FAO codes
[2016-07-25 16:14:54]  Proportion of tradeflows with nonmapped HS-codes: 88.1%
[2016-07-25 16:14:54]  Share of value of tradeflows with nonmapped HS-codes in total value: 94.4%
[2016-07-25 16:15:06]  [20697] Converting from comtrade to FAO codes
[2016-07-25 16:26:31]  Proportion of HS-codes not converted in FCL: 31.5%
[2016-07-25 16:26:33]  Proportion of tradeflows with nonmapped HS-codes: 46.3%
[2016-07-25 16:26:33]  Share of value of tradeflows with nonmapped HS-codes in total value: 30.8%
...
```

```
...
Proportion of HS-codes not converted in FCL: 31.5%
Proportion of HS-codes not converted in FCL: 31.5%
[2016-07-25 16:28:52]  Proportion of tradeflows with nonmapped HS-codes: 46.3%
[2016-07-25 16:28:52]  Share of value of tradeflows with nonmapped HS-codes in total value: 30.8%
[2016-07-25 16:28:54]  Proportion of tradeflows with nonmapped HS-codes: 46.3%
[2016-07-25 16:28:54]  Share of value of tradeflows with nonmapped HS-codes in total value: 30.8%
[2016-07-25 16:28:55]  Proportion of HS-codes not converted in FCL: 31.5%
[2016-07-25 16:28:57]  Proportion of tradeflows with nonmapped HS-codes: 46.3%
[2016-07-25 16:28:57]  Share of value of tradeflows with nonmapped HS-codes in total value: 30.8%
```

### 2016-09-21

- EUROSTAT data (that we use) versus the EU national country data that ARE in COMTRADE: Has an analysis been carried out by UNSD on any data differences? What are the reasons that UNSD does not use EUROSTAT data?

Regarding the Eurostat vs. National, it's due to differences in community vs. national concept. For your reference, see para. 10.9 of IMTS 2010 Compilers Manual below: 

10.9. Community versus national concept. In some instances, the EU concept 
diverges from the international recommendations. However, many member States 
simultaneously compile their data according to the so-called national concept which is 
usually more in line with the international recommendations. The principal differences 
between the EU concept and national concepts entail: (a) breakdown by partner 
country: for arrivals, certain member States record the country of origin as the partner 
country, whereas the member State of consignment appears in the EU statistics relating 
to the same movements; (b) treatment of goods in transit: some member States do 
not record goods, which they consider to be “in transit” in their national figures. This 
involves, first, imports from non-member countries that are cleared in these member 
States before being dispatched to other member States and, second, goods from other 
member States that are immediately re-exported to non-member countries. These 
flows are included in the EU statistics under intra- or extra-EU trade, as appropriate. 
The phenomenon is sometimes referred to as the “Rotterdam effect”;and (c) general 
trade: some member States compile extra-EU trade statistics according to the general 
trade system, while the EU concept is based on special trade (relax definition). 

### 2016-07-28 Transfer of Module

#### what preliminary analysis it does

#### what are the operations on COMTRADE data

#### what are the operations on Eurostat data

#### how do the various mapping operations (on country codes, item codes, units) work

#### how are EU records excluded from the UNSD file

#### where are the unmapped records stored? (countries and items with no match in our lists) How can they be retrieved and analysed if needed?

#### how can the outlier detection test be calibrated

see `out.coef` parameter in `complete_tf_cpc/metadata.xml` or [github search: "out.coef"](https://github.com/SWS-Methodology/faoswsTrade/search?utf8=%E2%9C%93&q=out.coef)  

```
# Coefficient for outlier detection
# See coef argument in ?boxplot.stats
```

#### what median values are used to correct outliers (by reporting country or reporting-partner country level)

#### how and where are Eurostat and UNSD data merged 

#### how does the aggregation into FCL work

#### at what stage is the conversion from the FCL to the CPC applied

#### how does the module assign flags to trade flows in CPC

not addressed in documentation

#### how does the module assign flags to total trade in CPC

not addressed in documentation

#### where are the mapping tables and what problems do they have

#### Marco started developing the semi-automatic mapping of new codes for 2014 data. What were his preliminary ideas. Is there a script in progress?

not clearly described in documentation: done or in progress? ask to provide draft code if exists

#### document "self trade"

#### how were "suspicious" notes/adjustments identified? (see attached email from yesterday)

#### why is the module returning (slightly) different results after each run for the same year?

#### correspondence table applied by country: transform comtrade M49 country codes -> faostat country codes -> M49

A number of comtrade countries are assigned to country 252 ("unknown"). 

- extract country codes and labels of countries that fall in this category
- extract values to have an idea of magnitude of the filter
- see if the mapping through faostat country codes can be bypassed
