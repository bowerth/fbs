---
layout: curriculum
title:  Screening Input Data Sources
byline: Summary reports for input data sources used by the statistical modules
---

## Observation Count

{% include rmarkdown_fragment/faoswsTrade/fragment_spark_count_reporter_partner.html %}

## Dimension Member Change

{% include rmarkdown_fragment/faoswsTrade/fragment_preprocessing_sql.html %}


## Workflow

The workflow diagram informs about the various steps of the pre-processing

**SWS Data**

  1. use R `faosws` to retrieve datatables for each year from SWS (approx. 15-25 minutes per table, total around 30 tables)
  2. save to R native format `rds` to preserve data types
  3. export to csv files and compress using gzip

**Processing (Spark)**

  1. load data for a range of years from both data sources (Eurostat CN8 and UNSD Tariffline) and store in parquet format, partitioned by year
  2. create SparkSQL view from partitioned parquet folders and execute SparkSQL query
  3. export query result to csv file

**dryworkflow (R)**

  1. set up routine that detects changes in result created by Spark routine using dryworkflow / Makefiles
  2. load SparkSQL query result csv data, perform summary statistics and create data plots
  3. use `html_fragment` as export type in rmarkdown; this will create an HTML page without a header that can be used in Jekyll

**Website (Jekyll)**

  1. use import batch script to check for modified files in dryworkflow folders
  2. make a minor modification to the markdown file where the `html_fragment` is included to trigger jekyll update
  3. if `jekyll serve` is running, the contents of `_site` directory will be updated automatically
  4. export modified contents to `sws_r_share/fbsmodules` using `rsync`

![Diagram re-processing workflow]({{ site.baseurl }}/assets/diagram/diagram-preprocessing-workflow.svg)

**Resources**

The various source files for Jekyll and dryworkflow have been copied to a network location

- T:\Team\_working\_folder\A\werthb\dryworkflow\_faoswsFBS
- T:\Team\_working\_folder\A\werthb\dryworkflow\_faoswsTrade
- T:\Team\_working\_folder\A\werthb\jekyll\_fbsmodules
