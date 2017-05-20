---
layout: curriculum
title:  FBS Estimation Modules
byline: Methodology implemented in statistical modules designed for FBS estimation
---

## SUA Module Graph

![sua-network-graph]({{ site.baseurl }}/assets/diagram/2016-07-13-sua-network-graph.svg)

## SUA Module Invalidation

### Re-run Trade Module

![sua-network-graph-trade]({{ site.baseurl }}/assets/diagram/2016-07-14-sua-network-graph-trade.svg)

### Re-run Trade and Production Modules

Hold re-run of `Food`, `Stock`, `Loss` and `Feed` modules until both `Trade` and `Production` modules have completed

![sua-network-graph-trade-production]({{ site.baseurl }}/assets/diagram/2016-07-14-sua-network-graph-trade-production.svg)

### Re-run Production and Food Modules

![sua-network-graph-production-food]({{ site.baseurl }}/assets/diagram/2016-07-14-sua-network-graph-production-food.svg)

## Production Module

### Flowchart Production Module

<!-- URL: [Production Workflow](https://raw.githubusercontent.com/SWS-Methodology/faoswsProduction/master/production_workflow_horizontal.jpg) -->

<!-- ![production_workflow_horizontal](https://raw.githubusercontent.com/SWS-Methodology/faoswsProduction/master/production_workflow_horizontal.jpg)
 -->

<!-- <img src="https://raw.githubusercontent.com/SWS-Methodology/faoswsProduction/master/production_workflow_horizontal.jpg" alt="production_workflow_horizontal" width="950px">  -->

yEd file: [2016-06-20-faoswsProduction.graphml]({{ site.baseurl }}/assets/diagram/2016-06-20-faoswsProduction.graphml)

![module-production-yed]({{ site.baseurl }}/assets/diagram/2016-06-20-faoswsProduction.svg)

<!-- URL: [Production Module Flow](https://cloud.githubusercontent.com/assets/1054320/15193239/18f489fc-17bd-11e6-9f3b-282c4891a702.png) -->
<!-- URL: [Production Module Flow](http://knsv.github.io/mermaid/live_editor/#/edit/Z3JhcGggVEIKCnN1YmdyYXBoIFByb2R1Y3Rpb24gRGF0YQpwcm9kWyJSYXcgQWdyaWN1bHR1cmFsIFByb2R1Y3Rpb24iXQplbmQKCnN1YmdyYXBoIElucHV0cwpwcm9kWyJSYXcgQWdyaWN1bHR1cmFsIFByb2R1Y3Rpb24iXQphbmltYWxfbWVhdF9tYXBwaW5nWyJBbmltYWwgTWVhdCBNYXBwaW5nIFRhYmxlIChjc3YgZmlsZSBvbiBzaGFyZWQgZHJpdmUpIl0KZmxhZ190YWJsZVsiRmxhZyBUYWJsZSAoRGF0YSBpbiBmYW9zd3NGbGFnIHBhY2thZ2UpIl0KeWllbGRfZm9ybXVsYVsiWWllbGQgRm9ybXVsYSAoRGF0YXRhYmxlKSJdCmNvbXBsZXRlX2ltcHV0YXRpb25fa2V5WyJJbXB1dGF0aW9uIGxpc3QgKGhhcmQgY29kZWQgaW4gZnVuY3Rpb24gZ2V0TWFpbktleSkiXQpyYXRpbwpzaGFyZQplbmQKCnN1YmdyYXBoIE1vZHVsZXMKc3ViZ3JhcGggSW1wdXRlIFNsYXVnaHRlcmVkCnByb2QgLS0-IGltcHV0ZV9zbGF1Z2h0ZXJlZF9tb2R1bGVbIlIgbW9kdWxlIl0KYW5pbWFsX21lYXRfbWFwcGluZyAtLT4gaW1wdXRlX3NsYXVnaHRlcmVkX21vZHVsZVsiUiBtb2R1bGUiXQpmbGFnX3RhYmxlIC0tPiBpbXB1dGVfc2xhdWdodGVyZWRfbW9kdWxlWyJSIG1vZHVsZSJdCnlpZWxkX2Zvcm11bGEgLS0-IGltcHV0ZV9zbGF1Z2h0ZXJlZF9tb2R1bGVbIlIgbW9kdWxlIl0KaW1wdXRlX3NsYXVnaHRlcmVkX21vZHVsZVsiUiBtb2R1bGUiXSAtLT4gaW1wdXRlZF9zbGF1Z2h0ZXJlZF9kYXRhWyJJbXB1dGVkIFNsYXVnaHRlcmVkIERhdGEiXQplbmQKCnN1YmdyYXBoIFN5bmNocm9uaXNlIFNsYXVnaHRlcmVkCmltcHV0ZWRfc2xhdWdodGVyZWRfZGF0YVsiSW1wdXRlZCBTbGF1Z2h0ZXJlZCBEYXRhIl0gLS0-IHN5bmNocm9uaXNlX3NsYXVnaHRlcmVkX21vZHVsZVsiUiBtb2R1bGUiXQphbmltYWxfbWVhdF9tYXBwaW5nIC0tPiBzeW5jaHJvbmlzZV9zbGF1Z2h0ZXJlZF9tb2R1bGVbIlIgbW9kdWxlIl0KZmxhZ190YWJsZSAgLS0-IHN5bmNocm9uaXNlX3NsYXVnaHRlcmVkX21vZHVsZVsiUiBtb2R1bGUiXQpyYXRpby0tPiBzeW5jaHJvbmlzZV9zbGF1Z2h0ZXJlZF9tb2R1bGVbIlIgbW9kdWxlIl0Kc2hhcmUtLT4gc3luY2hyb25pc2Vfc2xhdWdodGVyZWRfbW9kdWxlWyJSIG1vZHVsZSJdCnN5bmNocm9uaXNlX3NsYXVnaHRlcmVkX21vZHVsZS0tPiBzeW5jaHJvbmlzZWRfc2xhdWdodGVyZWRfZGF0YVsiU3luY2hyb25pc2VkIFNsYXVnaHRlcmVkIERhdGEiXQplbmQKCnN1YmdyYXBoIEJhbGFuY2UgUHJvZHVjdGlvbiBJZGVudGl0eQpzeW5jaHJvbmlzZWRfc2xhdWdodGVyZWRfZGF0YVsiU3luY2hyb25pc2VkIFNsYXVnaHRlcmVkIERhdGEiXSAtLT4gYmFsYW5jZV9wcm9kdWN0aW9uX2lkZW50aXR5X21vZHVsZVsiUiBtb2R1bGUiXQp5aWVsZF9mb3JtdWxhIC0tPiBiYWxhbmNlX3Byb2R1Y3Rpb25faWRlbnRpdHlfbW9kdWxlWyJSIG1vZHVsZSJdCmJhbGFuY2VfcHJvZHVjdGlvbl9pZGVudGl0eV9tb2R1bGVbIlIgbW9kdWxlIl0gLS0-IGJhbGFuY2VkX2RhdGFbIkJhbGFuY2VkIERhdGEiXQplbmQKCnN1YmdyYXBoIEJ1aWxkIEltcHV0ZWQgRGF0YXNldApiYWxhbmNlZF9kYXRhWyJCYWxhbmNlZCBEYXRhIl0gLS0-IGJ1aWxkX2ltcHV0ZWRfZGF0YXNldF9tb2R1bGVbIlIgbW9kdWxlIl0KYW5pbWFsX21lYXRfbWFwcGluZyAtLT4gYnVpbGRfaW1wdXRlZF9kYXRhc2V0X21vZHVsZVsiUiBtb2R1bGUiXQpjb21wbGV0ZV9pbXB1dGF0aW9uX2tleSAtLT4gYnVpbGRfaW1wdXRlZF9kYXRhc2V0X21vZHVsZVsiUiBtb2R1bGUiXQp5aWVsZF9mb3JtdWxhIC0tPiBidWlsZF9pbXB1dGVkX2RhdGFzZXRfbW9kdWxlWyJSIG1vZHVsZSJdCmJ1aWxkX2ltcHV0ZWRfZGF0YXNldF9tb2R1bGUtLT4gaW1wdXRlZF9vYmplY3RzWyJJbXB1dGVkIE9iamVjdHMgKE9uIFNXUyBTaGFyZWQgRHJpdmUpIl0KZW5kCgpzdWJncmFwaCBGaWxsIEltcHV0YXRpb24KaW1wdXRlZF9vYmplY3RzWyJJbXB1dGVkIE9iamVjdHMgKE9uIFNXUyBTaGFyZWQgRHJpdmUpIl0gLS0-IGZpbGxfaW1wdXRhdGlvbl9tb2R1bGVbIlIgbW9kdWxlIl0KZmlsbF9pbXB1dGF0aW9uX21vZHVsZSAtLT4gaW1wdXRlZF9kYXRhc2V0c1siRnVsbHkgSW1wdXRlZCBEYXRhc2V0Il0KZW5kCmVuZA) -->

<!-- ![Production Flow Chart](https://cloud.githubusercontent.com/assets/1054320/15193239/18f489fc-17bd-11e6-9f3b-282c4891a702.png) -->
<!-- ![Production Flow Chart](/assets/diagram/production-flowchart-mermaid.svg) -->

<!-- <iframe src="http://knsv.github.io/mermaid/live_editor/#/view/Z3JhcGggVEIKCnN1YmdyYXBoIFByb2R1Y3Rpb24gRGF0YQpwcm9kWyJSYXcgQWdyaWN1bHR1cmFsIFByb2R1Y3Rpb24iXQplbmQKCnN1YmdyYXBoIElucHV0cwpwcm9kWyJSYXcgQWdyaWN1bHR1cmFsIFByb2R1Y3Rpb24iXQphbmltYWxfbWVhdF9tYXBwaW5nWyJBbmltYWwgTWVhdCBNYXBwaW5nIFRhYmxlIChjc3YgZmlsZSBvbiBzaGFyZWQgZHJpdmUpIl0KZmxhZ190YWJsZVsiRmxhZyBUYWJsZSAoRGF0YSBpbiBmYW9zd3NGbGFnIHBhY2thZ2UpIl0KeWllbGRfZm9ybXVsYVsiWWllbGQgRm9ybXVsYSAoRGF0YXRhYmxlKSJdCmNvbXBsZXRlX2ltcHV0YXRpb25fa2V5WyJJbXB1dGF0aW9uIGxpc3QgKGhhcmQgY29kZWQgaW4gZnVuY3Rpb24gZ2V0TWFpbktleSkiXQpyYXRpbwpzaGFyZQplbmQKCnN1YmdyYXBoIE1vZHVsZXMKc3ViZ3JhcGggSW1wdXRlIFNsYXVnaHRlcmVkCnByb2QgLS0-IGltcHV0ZV9zbGF1Z2h0ZXJlZF9tb2R1bGVbIlIgbW9kdWxlIl0KYW5pbWFsX21lYXRfbWFwcGluZyAtLT4gaW1wdXRlX3NsYXVnaHRlcmVkX21vZHVsZVsiUiBtb2R1bGUiXQpmbGFnX3RhYmxlIC0tPiBpbXB1dGVfc2xhdWdodGVyZWRfbW9kdWxlWyJSIG1vZHVsZSJdCnlpZWxkX2Zvcm11bGEgLS0-IGltcHV0ZV9zbGF1Z2h0ZXJlZF9tb2R1bGVbIlIgbW9kdWxlIl0KaW1wdXRlX3NsYXVnaHRlcmVkX21vZHVsZVsiUiBtb2R1bGUiXSAtLT4gaW1wdXRlZF9zbGF1Z2h0ZXJlZF9kYXRhWyJJbXB1dGVkIFNsYXVnaHRlcmVkIERhdGEiXQplbmQKCnN1YmdyYXBoIFN5bmNocm9uaXNlIFNsYXVnaHRlcmVkCmltcHV0ZWRfc2xhdWdodGVyZWRfZGF0YVsiSW1wdXRlZCBTbGF1Z2h0ZXJlZCBEYXRhIl0gLS0-IHN5bmNocm9uaXNlX3NsYXVnaHRlcmVkX21vZHVsZVsiUiBtb2R1bGUiXQphbmltYWxfbWVhdF9tYXBwaW5nIC0tPiBzeW5jaHJvbmlzZV9zbGF1Z2h0ZXJlZF9tb2R1bGVbIlIgbW9kdWxlIl0KZmxhZ190YWJsZSAgLS0-IHN5bmNocm9uaXNlX3NsYXVnaHRlcmVkX21vZHVsZVsiUiBtb2R1bGUiXQpyYXRpby0tPiBzeW5jaHJvbmlzZV9zbGF1Z2h0ZXJlZF9tb2R1bGVbIlIgbW9kdWxlIl0Kc2hhcmUtLT4gc3luY2hyb25pc2Vfc2xhdWdodGVyZWRfbW9kdWxlWyJSIG1vZHVsZSJdCnN5bmNocm9uaXNlX3NsYXVnaHRlcmVkX21vZHVsZS0tPiBzeW5jaHJvbmlzZWRfc2xhdWdodGVyZWRfZGF0YVsiU3luY2hyb25pc2VkIFNsYXVnaHRlcmVkIERhdGEiXQplbmQKCnN1YmdyYXBoIEJhbGFuY2UgUHJvZHVjdGlvbiBJZGVudGl0eQpzeW5jaHJvbmlzZWRfc2xhdWdodGVyZWRfZGF0YVsiU3luY2hyb25pc2VkIFNsYXVnaHRlcmVkIERhdGEiXSAtLT4gYmFsYW5jZV9wcm9kdWN0aW9uX2lkZW50aXR5X21vZHVsZVsiUiBtb2R1bGUiXQp5aWVsZF9mb3JtdWxhIC0tPiBiYWxhbmNlX3Byb2R1Y3Rpb25faWRlbnRpdHlfbW9kdWxlWyJSIG1vZHVsZSJdCmJhbGFuY2VfcHJvZHVjdGlvbl9pZGVudGl0eV9tb2R1bGVbIlIgbW9kdWxlIl0gLS0-IGJhbGFuY2VkX2RhdGFbIkJhbGFuY2VkIERhdGEiXQplbmQKCnN1YmdyYXBoIEJ1aWxkIEltcHV0ZWQgRGF0YXNldApiYWxhbmNlZF9kYXRhWyJCYWxhbmNlZCBEYXRhIl0gLS0-IGJ1aWxkX2ltcHV0ZWRfZGF0YXNldF9tb2R1bGVbIlIgbW9kdWxlIl0KYW5pbWFsX21lYXRfbWFwcGluZyAtLT4gYnVpbGRfaW1wdXRlZF9kYXRhc2V0X21vZHVsZVsiUiBtb2R1bGUiXQpjb21wbGV0ZV9pbXB1dGF0aW9uX2tleSAtLT4gYnVpbGRfaW1wdXRlZF9kYXRhc2V0X21vZHVsZVsiUiBtb2R1bGUiXQp5aWVsZF9mb3JtdWxhIC0tPiBidWlsZF9pbXB1dGVkX2RhdGFzZXRfbW9kdWxlWyJSIG1vZHVsZSJdCmJ1aWxkX2ltcHV0ZWRfZGF0YXNldF9tb2R1bGUtLT4gaW1wdXRlZF9vYmplY3RzWyJJbXB1dGVkIE9iamVjdHMgKE9uIFNXUyBTaGFyZWQgRHJpdmUpIl0KZW5kCgpzdWJncmFwaCBGaWxsIEltcHV0YXRpb24KaW1wdXRlZF9vYmplY3RzWyJJbXB1dGVkIE9iamVjdHMgKE9uIFNXUyBTaGFyZWQgRHJpdmUpIl0gLS0-IGZpbGxfaW1wdXRhdGlvbl9tb2R1bGVbIlIgbW9kdWxlIl0KZmlsbF9pbXB1dGF0aW9uX21vZHVsZSAtLT4gaW1wdXRlZF9kYXRhc2V0c1siRnVsbHkgSW1wdXRlZCBEYXRhc2V0Il0KZW5kCmVuZA" width = "100%" style="border: 1px solid #AAA; height: 51em"></iframe> -->

<!-- ![module-production-drawio]({{ site.baseurl }}/assets/diagram/module-production-drawio.svg)
 -->

### Flowchart Livestock Imputation

Public file: [livestock_flow.jpg](https://raw.githubusercontent.com/SWS-Methodology/faoswsProduction/master/modules/impute_livestock/livestock_flow.jpg)

yEd file: [2016-06-20-faoswsProduction-livestock.graphml]({{ site.baseurl }}/assets/diagram/2016-06-20-faoswsProduction-livestock.graphml)

![module-production-livestock-yed]({{ site.baseurl }}/assets/diagram/2016-06-20-faoswsProduction-livestock.svg)

## Stock Module

### Flowchart Stock Module

<!-- URL: [Stock Flowchart.html](https://www.draw.io/#G0B_RnVCJ7CNm7RHBQTHMwZ0VUNGs) -->
<!-- yEd file: [2016-05-13-faoswsStock.graphml]({{ site.baseurl }}/assets/diagram/2016-07-13-faoswsStock.graphml) -->
yEd file: [2016-09-05-faoswsStock.graphml]({{ site.baseurl }}/assets/diagram/2016-09-05-faoswsStock.graphml)

Report AMIS: [2016-05-18-stocks-amis.pdf]({{ site.baseurl }}/assets/report/2016-05-18-stocks-amis.pdf)

<!-- ![module-stock-drawio]({{ site.baseurl }}/assets/diagram/module-stock-drawio.svg) -->
<!-- ![module-stock-yed]({{ site.baseurl }}/assets/diagram/2016-07-13-faoswsStock.svg) -->
![module-stock-yed]({{ site.baseurl }}/assets/diagram/2016-09-05-faoswsStock.svg)

{% include formula/stock-formula.md %}

## Tourist Module

### Flowchart tourist Module

URL: [Tourist Flowchart.html](https://www.draw.io/#G0B_RnVCJ7CNm7RHBQTHMwZ0VUNGs)

![module-tourist-drawio]({{ site.baseurl }}/assets/diagram/module-tourist-drawio.svg)

{% include formula/tourist-formula.md %}

## Food Module

### Compact Flowchart Food Module

![module-food-compact-yed]({{ site.baseurl }}/assets/diagram/2016-07-08-faoswsFood-compact.svg)

### Flowchart Food Module

![module-food-yed]({{ site.baseurl }}/assets/diagram/2016-06-09-faoswsFood.svg)

{% include formula/food-formula.md %}

## Industrial Use Module

### Flowchart Industrial Use Module

![module-industrial-use-yed]({{ site.baseurl }}/assets/diagram/2016-06-13-faoswsIndustrial.svg)

## Feed Module

## Loss Module

### Flowchart Loss Module

{% include formula/loss-formula.md %}

![network-repository]({{ site.baseurl }}/assets/diagram/network-repository.svg)

### git repository on network share

- monitor suggested changes (e.g. foodPerishableGroup.csv)
- use as development environment
- consider for integration with repository used by SWS

### Configuration

```
git remote add upstream https://github.com/SWS-Methodology/faoswsLoss.git
git remote set-url origin file://t:/Team_working_folder/A/FBS-Modules/faoswsLoss/.git
```

## Seed Module

## Trade Module

### Outlier Detection in "Complete Trade Flow" Module

{% include rmarkdown_fragment/faoswsTrade/fragment_complete_tf_cpc_tradedata_2011_rds.html %}

`coef` argument of [`boxplot.stats`](https://stat.ethz.ch/R-manual/R-devel/library/grDevices/html/boxplot.stats.html) R function in `grDevices`
:   determines how far the plot 'whiskers' extend out from the box. If `coef` is positive, the whiskers extend to the most extreme data point which is no more than `coef` times the length of the box away from the box. A value of zero causes the whiskers to extend to the data extremes (and no outliers be returned). The default value for `coef` is **1.5**. The interquartile range **IQR** corresponds to the length of the box, i.e. the difference between **Q1** and **Q3**.

![Boxplot_vs_PDF.svg](https://upload.wikimedia.org/wikipedia/commons/1/1a/Boxplot_vs_PDF.svg)

Source: [https://en.wikipedia.org/wiki/Box_plot#/media/File:Boxplot_vs_PDF.svg](https://en.wikipedia.org/wiki/Box_plot#/media/File:Boxplot_vs_PDF.svg)

[faoswsTrade/modules/complete_tf_cpc/main.R](https://github.com/SWS-Methodology/faoswsTrade/blob/master/modules/complete_tf_cpc/main.R)

```r
# Outlier detection

tradedata <- tradedata %>%
  group_by_(~year, ~reporter, ~flow, ~hs) %>%
  mutate_(
    uv_reporter = ~median(uv, na.rm = T),
    outlier = ~uv %in% boxplot.stats(uv, coef = out_coef, do.conf = F)$out) %>%
  ungroup()
```

### Adjustment Notes applied to Comtrade

{% include rmarkdown_fragment/fragment_adjustments_csv.html %}

Visual display of numeric weight distribution by type of trade flow. Log values are shown for better display.

![report-adjustments-csv-pirateplot-1]({{ site.baseurl }}/assets/dryworkflow/report-adjustments-csv-pirateplot-1.png)
![report-adjustments-csv-pirateplot-2]({{ site.baseurl }}/assets/dryworkflow/report-adjustments-csv-pirateplot-2.png)

Based on the filter in the module, two files have been prepared

```
adjustments = adjustments %>%
  filter_(~!(is.na(year) &
               weight == 1000))
```

- 1726 observations where `weight` is equal to `1000`: [adjustments_weigth1000.csv](T:\Team_working_folder\A\FBS-Modules\Trade module\adjustments_weigth1000.csv)
- 1599 observations where `weight` is equal to `1000` and `year` is specified: [adjustments_weigth1000_year.csv](T:\Team_working_folder\A\FBS-Modules\Trade module\adjustments_weigth1000_year.csv)

I.e. there are only 127 out of the 1726 observations where no year is specified. This corresponds to 7.3 % of the observations.

### Flowchart Trade Module

#### Raw Data Transformation

[SWS-Methodology/faoswsTrade/vignettes/Documentation/assets/trade\_1.png](https://github.com/SWS-Methodology/faoswsTrade/blob/master/vignettes/Documentation/trade_1.svg)

<img src="https://cdn.rawgit.com/SWS-Methodology/faoswsTrade/master/vignettes/Documentation/assets/trade_1.png" alt="module-trade-github-trade_1" width="500px"> 

#### Imputation and Aggregation

[SWS-Methodology/faoswsTrade/vignettes/Documentation/assets/trade\_1\_bis.png](https://github.com/SWS-Methodology/faoswsTrade/blob/master/vignettes/Documentation/assets/trade_1_bis.png)

<img src="https://cdn.rawgit.com/SWS-Methodology/faoswsTrade/master/vignettes/Documentation/assets/trade_1_bis.png" alt="module-trade-github-trade_1_bis" width="500px"> 

## Standardization Module

### Flowchart Standardization Module

![module-standardization-yed]({{ site.baseurl }}/assets/diagram/2016-06-08-faoswsStandardization.svg)

## Imputation Module

## Balancing Module

## Flag Module

## Util Module

## Modules Module

## GitHub Issues by Repository

{% include dryworkflow/list-issues.md %}

## Issues PDF by Repository

The following links can be accessed after logging in to hostedredmine.com
:   user: `faoessatest`  
    login: `5udSPY57`

- Food [food-module/issues.pdf](http://hostedredmine.com/projects/food-module/issues.pdf?query_id=6543)

- Stocks [stocks-module/issues.pdf](http://hostedredmine.com/projects/stocks-module/issues.pdf?query_id=6543)

- Tourist [tourist-module/issues.pdf](http://hostedredmine.com/projects/tourist-module/issues.pdf?query_id=6543)

- Industrial Use [industrial-use/issues.pdf](http://hostedredmine.com/projects/industrial-use/issues.pdf?query_id=6543)

## Sub-Modules by Package

Each of the subfolders in `/modules` is supposed to contain a `main.R` and a `metadata.xml` file

{% include dryworkflow/list-modules.md %}

## R Scripts by Package

{% include dryworkflow/r-functions.md %}
