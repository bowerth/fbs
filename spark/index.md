---
layout: curriculum
title:  Spark Documentation
byline: Step-by-step documentation how run Spark SQL queries on trade raw data
---

## About Apache Spark

Apache Spark is a fast and general engine for large-scale data processing. This allows to process more data than fits into RAM, the main limitation when using R. Commercial statistical tools such as SPSS and SAS are not constrained by RAM: observations are loaded, processed and removed sequentially. Recent versions of RStudio, a popular IDE for R, includes an interface to Spark. However, this is complicated to set up on Windows with limited user privileges.


## Data Preparation

In order to use Spark for processing local data, we need to store information in compressed text file format

- extract Eurostat CN8 and UNSD Tariffline datatables from SWS and save in `rds` format using R dryworkflow
- use R dryworkflow to read `rds` files and export to compressed `csv` files in `gz` format


## Remote Setup

The shortest way to execute SQL queries is offered by the databricks platform in combination with Amazon S3.

### Amazon S3

User Login
:   URL: [https://058644585154.signin.aws.amazon.com/console](https://058644585154.signin.aws.amazon.com/console)  
    User: `tradeuser`  
    Password: `f!3P)oDl7!5%`  
    AWS_ACCESS_KEY_ID: `AKIAJLC5BRWMJD5VN2HA`  
    AWS_SECRET_ACCESS_KEY: `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`

- create bucket in region US-West-2 (Oregon) to minimize transfer for the databricks platform
- upload compressed csv files to this Amazon S3 bucket
- create empty folder for each data source
- create parquet files for both data sources using `write-parquet-s3.scala` notebook

### Databricks

Databricks is an online platform that allows using Spark interactively with minimum investment. The community edition is free of charge that starts small Spark clusters on Amazon AWS with 6GB memory. This is sufficient to convert the data and run queries.

#### Register

We need to register on a per-user basis because an email address is required for user authetication

- register for the databricks community edition at [databricks.com](https://databricks.com/try-databricks)

#### Convert data for remote use

In order to execute queries on the complete time series, information must be stored in a different format. Data has already been uploaded to Amazon S3. In case the input data changes, the conversion of raw data to parquet format must be repeated.

- use `LoadDataDS` procedure from Spark to read `gz` files and save to `parquet` files on local disk
- public link to notebook: [write-parquet-s3](https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/4610059781407782/3278022976594753/8885677949701821/latest.html) **contains passwords, do not share**

#### Test Query

The test query schedules multiple jobs executed by the cluster's worker nodes. The execution can be tracked with different tools. The result is displayed in the web browser and can be copied manually to a text file for further processing.

- public link to notebook: [s3-sql-query](https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/4610059781407782/1607078090355792/8885677949701821/latest.html) **contains passwords, do not share**


## Local Setup

### JDK

In order to compile classes for the JVM, we need a JDK

- download the latest JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html), e.g. `jdk-8u111-windows-x64.exe`
- open the downloaded exe file using [7zip](http://www.7-zip.org/)
- go to the directory `.rsrc/1033/JAVA_CAB10/`
- the only file there is `111`, which is also a zipped file containing `tools.zip`. Extract this file to get `tools.zip`
- so now perform the original unpack process, by unzipping `tools.zip` to your desired Java installation path
- do the same for Java source `src.zip` is the file `110` at `.rsrc/1033/JAVA_CAB9`
- copy `src.zip` to the java installation path where `tools.zip` has been unzipped
- set environment variables `JAVA_HOME` and `JDK_HOME` to the installation path

### Lightbend Activator

Spark is implemented in Scala. Running and modifying a Spark App locally requires re-compiling the class files for execution on the JVM. Lightbend Activator is a build tool for Scala that can be used in Windows.

- download Activator from [Lightbend](https://www.lightbend.com/activator/download)
- extract to local disk and add folder location to `PATH` environment variable

### Install Spark

Next we download and install a pre-compiled version of Spark including Hadoop

- download latest Spark release from [spark.apache.org](http://spark.apache.org/downloads.html)
- extract to local disk
- set environment variable `SPARK_HOME`

### Convert data for local use

In order to execute queries on the complete time series, information must be stored in [parquet file format](https://parquet.apache.org/)

- use `LoadDataDS` procedure from Spark to read `gz` files and save to `parquet` files on local disk

### Test Query

An example application to execute a Spark SQL query is available on github

- clone the [sparkDemo](https://github.com/bowerth/sparkDemo/) repository
- open cmd Windows terminal
- go to the root folder and execute `activator`
- exit activator with `exit` command
- run a sample query, e.g. `activator "run-main controller.query.QueryDataDS ct_tariffline_unlogged chapter spark_count_ct_tl_chapter.csv"`
- other sample queries can be found in the [QueryDataDS.scala](https://github.com/bowerth/sparkDemo/blob/master/src/main/scala/QueryDataDS.scala) script
