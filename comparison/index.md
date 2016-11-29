---
layout: curriculum
title:  Comparing FBS results
byline: Compare output from modules with published statistics
---

## Introduction

### How to read the visualization

- data for countries contained in each region are sorted in descending order according to their maximum value
- from the top to the bottom, the color of lines gets brighter, exhibiting countries with smaller absolute values
- colors are mapped to values according to the log scale as can be seen from the legend on the right-hand side of each visualization
- bright cells within a series of dark cells indicate possible issues with the quality of information (and vice versa dark cells within a series of bright cells)
- zero values have been replaced with NA and show as 0 in the plot

### Grouping of countries

- visualizations are shown for macro geographical (continental) regions obtained from UNSD [m49regin.htm](http://unstats.un.org/unsd/methods/m49/m49regin.htm)

### Distinguish zero and missing values

- in order to distinguish zero values (white) from missing values (transparent), it is suggested to use a background color inverter, for example [Simple Night Mode](https://addons.mozilla.org/it/firefox/addon/simple-night-mode/) for Mozilla Firefox or [Night Mode Pro](https://chrome.google.com/webstore/detail/night-mode-pro/gbilbeoogenjmnabenfjfoockmpfnjoh) for Google Chrome

## Visualization of Trade Module Output wo notes

- data shown below has been generated using the Trade Module (skipping adjustment notes)

{% include rmarkdown_fragment/faoswsTrade/fragment_total_trade_cpc_rds.html %}

## Visualization of Trade Module Output w notes

- data shown below has been generated using the Trade Module (adjustment notes applied to Comtrade / Eurostat sources) 

{% include rmarkdown_fragment/faoswsTrade/fragment_sws_trade_total_trade_cpc_m49.html %}

## Visualization of Published Trade Data

- data shown below has been downloaded from [FAOSTAT Crops and livestock product All Data Normalized](http://fenix.fao.org/faostat/beta/en/#data/TP)
- values are: Import Quantity (element code 5610), unit "tonnes"

{% include rmarkdown_fragment/faoswsTrade/fragment_faostat_trade_crops_livestock_csv.html %}

## Response Ignore Notes

{% include rmarkdown_fragment/faoswsTrade/fragment_missing_values_total_trade_cpc.html %}


## Visualization of Complete Trade Flow

### Top 20 countries wheat imports

The visualization shows quantities of commodity `111`, measured element `5610`.

{% include rmarkdown_fragment/faoswsTrade/fragment_complete_trade_flow_cpc_2011_csv.html %}

![fragment-complete-trade-flow-cpc-2011-csv-plot-colors-1.png]({{ site.baseurl }}/assets/dryworkflow/faoswsTrade/fragment-complete-trade-flow-cpc-2011-csv-plot-colors-1.png)

