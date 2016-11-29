---
layout: curriculum
title:  Site Build Documentation
byline: Step-by-step documentation how the website can be built and modified
---

## Installation

### Ruby + Jekyll

The website is created from markdown files rendered to html by Jekyll

- this site explains how Jekyll can be used on Windows: [Run Jekyll on Windows](http://jekyll-windows.juthilo.com/)
- download and install Ruby (64bit) from [rubyinstaller.org](http://rubyinstaller.org/downloads/)
- add ruby path to `PATH` environment variable `C:\Users\[Username]\Programs\Ruby21-x64`
- download and install the Ruby DevKit (64bit) from the same page, search **For use with Ruby 2.0 and above (x64 - 64bits only)**
- install Jekyll `gem install jekyll`
- open a git bash terminal and navigate to Jekyll root folder
- install Jekyll dependencies `bundle exec install`
- serve the site locally `bundle exec jekyll serve`
- export contents to sws\_r\_share: `rsync -h -v -P -t -u --recursive /cygdrive/c/Users/[Username]/path/to/_site/* //hqlprsws1.hq.un.fao.org/sws_r_share/fbsmodules`

### Git bash + Make

The contents of the website are created and updated using R scripts that are triggered by `Makefiles`

- the folder structure based on [dryworkflow](https://github.com/petebaker/dryworkflow)
- the `Makefile` in the root directory indicates subfolders that are checked for additional `Makefiles`
- the Makefile definitions for R can be found at [r-rules.mk](https://github.com/petebaker/r-makefile-definitions/blob/master/r-rules.mk)
- open a git bash terminal and navigate to dryworkflow root folder
- execute `make`

## Modify Contents

### Diagrams

The website includes a number of diagrams that facilitate understanding the project structure

- most diagrams have been created using yEd, an open source diagram editor [yWorks yEd Graph Editor](http://www.yworks.com/products/yed)
- `.graphml` files are located at `/assets/diagram/`
- to include in the jekyll website, diagrams are exported from yEd in `svg` format
- to display in github and include in PDF documentation, `png` format is required 
- few diagrams have been created using the online tools draw.io and Google Drawings

### Visualizations

The heatmap visualization is using the R package **highcharter** that can only be used internally for licensing reasons

- `/extra/faostat_bulk.csv` specifies the datasets that are downloaded from FAOSTAT
- `/downloadData/download_faostat_bulk.R` downloads the data from the internet
- `/data/codebook/faostat_trade_crops_livestock_norm_codebook.csv` is the codebook for renaming variables
- `/readMergeData/read_codebook_faostat_trade_crops_livestock_norm.R` loads the codebook
- `/readMergeData/read_faostat_trade_crops_livestock_norm_csv.R` reads the downloaded CSV data and stores in RData format
- `/readMergeData/clean_faostat_trade_crops_livestock_norm_csv.R` applies the renaming specified in the codebook
- `/work/summary_faostat_trade_crops_livestock_norm_csv.R` subsets the data to selected commodities
- continental regions are defined in the `stanDim` list of objects contained in the [`stan`](https://github.com/bowerth/stan) package: `data(stanDim)`
- `/fragments/fragment_faostat_trade_crops_livestock_csv.Rmd` creates the html fragment for time series published on FAOSTAT

## Import Contents

Once the changes have been completed in the dryworkflow routine(s), the compiled html fragments files are imported to the Jekyll site. The contents of the `import-dryworkflow.bat` are shown below. In this example, fragments from two dryworkflow projects are integrated: one for all FBS, the other for trade-specific outputs.

```
set JEKYLLFAOCYG="/cygdrive/c/Users/[User]/path/to/jekyll/site"
set DRYFAOFBSCYG="/cygdrive/c/Users/[User]/path/to/dryworkflow/root"
set SWSDATA="/cygdrive/c/SWS-Data"

rsync -h -v -P -t --recursive %DRYFAOFBSCYG%/includes/* %JEKYLLFAOCYG%/_includes/dryworkflow/
rsync -h -v -P -t --recursive %DRYFAOFBSCYG%/figures/* %JEKYLLFAOCYG%/assets/dryworkflow/
rsync -h -v -P -t --recursive %DRYFAOFBSCYG%/fragments/*.html %JEKYLLFAOCYG%/_includes/rmarkdown_fragment/

rsync -h -v -P -t --recursive %SWSDATA%/faoswsTrade/fragments/*.html %JEKYLLFAOCYG%/_includes/rmarkdown_fragment/faoswsTrade/
rsync -h -v -P -t --recursive %SWSDATA%/faoswsTrade/figures/* %JEKYLLFAOCYG%/assets/dryworkflow/faoswsTrade/
```


