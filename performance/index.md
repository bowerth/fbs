---
layout: curriculum
title:  Producing Statistics
byline: Benchmark production performance in QA and Production environments
---

## Introduction

- The Trade Module operates on one year at a time
- To create a time series, it has to be run multiple times
- Each run of the module takes at least 80 to 100 minutes
- Reading data from and writing back to the Statistical Working System takes a considerable share of this time
- The period 2000-2014 is targeted for dissemination
- Test runs with varying number of parallel processes are performed in order to determine the minimum time to update the whole time series

## Setup

The following code is to set up a log to see CPU and memory consumption for all current Rserve processes:

```
echo '               DATE   PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM     TIME+  COMMAND' > testRservelog.txt
top -bd 30 -n 720 | grep Rserve | awk '{ print strftime("%Y-%m-%d_%H:%M:%S"), $0; fflush() }' >> testRservelog.txt &
```

The log is available at file://///hqlprsws1.hq.un.fao.org/sws_r_share/testRservelog.txt

{% include rmarkdown_fragment/report_sws_rserve_log_2_txt.html %}

{% include rmarkdown_fragment/report_sws_rserve_log_4_txt.html %}

{% include rmarkdown_fragment/report_sws_rserve_log_4_2009_txt.html %}

{% include rmarkdown_fragment/report_sws_rserve_log_8_txt.html %}

## Required ETL Time

![faoswsTrade ETL Time]({{ site.baseurl }}/assets/diagram/2016-09-27-faoswsTrade-ETL-Time.svg)

## QA Complete TF CPC 2000-2008

### Session IDs

2009
:   ca58cea9-78c1-464b-8336-40acb3f9f895

2008
:   3c41eedc-0291-45b2-b23e-3a94e6722592

2007
:   fda971eb-bce6-4d84-be22-395d7fa905fa

2006
:   013f2448-cb88-458f-8dae-287be2823e72

2005
:   c0aa8c8e-ec80-425c-8eab-c550c3188e4a

2004
:   934189da-3026-4980-b5a3-047a76c85d14

2003
:   fbdbf8ea-b1fe-4a9e-bb67-439f250c995d

2002
:   cd51f707-d38f-432a-8af5-8f62d5124906

2001
:   dd4b613e-7567-49ff-a18e-3e8162626b40

2000
:   63734bf5-9ecf-4fa7-a697-5784b0e94c8c

### Example Error Message

> `fclunits` object in faoswsTrade repository: [/data/#dataframe-faoswstrade-fclunits]({{ site.url }}{{ site.baseurl }}/data/#dataframe-faoswstrade-fclunits)
> created using [/data-raw/fclunits.R](https://github.com/SWS-Methodology/faoswsTrade/blob/master/data-raw/fclunits.R)

```
The plugin was launched over the following datasets:

 - completed_tf_cpc_m49 in domain trade

and with the following parameters:

 - year = 2003
 - out_coef = 1.5

The plugin started Fri, 5 Aug 2016 11:51:15 +0200 and ended Fri, 5 Aug 2016 12:34:26 +0200 with the following message:

	Error message from R: Error: cannot join on columns 'fcl' x 'fcl': index out of bounds 

 Stacktrace: 
stop(list(message = "cannot join on columns 'fcl' x 'fcl': index out of bounds ", .Call("dplyr_left_join_impl", PACKAGE = "dplyr", x, y, by_x, left_join_impl(x, y, by$x, by$y) left_join.tbl_df(., fclunits, by = "fcl") left_join(., fclunits, by = "fcl")
function_list[[k]](value)
withVisible(function_list[[k]](value))
freduce(value, `_function_list`)
`_fseq`(`_lhs`)
eval(expr, envir, enclos)
eval(quote(`_fseq`(`_lhs`)), env, env)
withVisible(eval(quote(`_fseq`(`_lhs`)), env, env)) esdata %>% left_join(fclunits, by = "fcl")
```