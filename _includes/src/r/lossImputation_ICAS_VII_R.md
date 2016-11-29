```{r}

rm(list=ls())
suppressMessages({
  #library(bit64)
  #library(curl)
  library(faosws)
  library(faoswsUtil)
  library(lme4)
  library(data.table)
  library(magrittr)
  library(reshape2)
  library(igraph)
  library(plyr)
  library(dplyr)
  library(ggplot2)
  #library(RJDBC)
})

updateModel = TRUE

setwd("C:/Users/Golini/Dropbox/FAO/ICAS VII/")

## Set up for the test environment and parameters

if(CheckDebug()) {
   if(Sys.info()["user"] == "Golini"){
    # Nata's work computer
    SetClientFiles(dir = "~/R certificate files/Production/")
    token = "e16a500b-2077-471b-8edf-6d810a85814d" # Nata's token 
    files = dir("~/Github/faoswsLoss/R",
                full.names = TRUE)
  } else {
    stop("User not yet implemented!")
  }

  GetTestEnvironment(
    ## baseUrl = "https://hqlqasws1.hq.un.fao.org:8181/sws",
    baseUrl = "https://hqlprswsas1.hq.un.fao.org:8181/sws",
    token = token
  )  
}




## Year should be a paramameter selected.
selectedYear = as.character(1991:2015)


areaVar = "geographicAreaM49"
areaVarFS = "geographicAreaFS"
yearVar = "timePointYears"
itemVar = "measuredItemCPC"
itemVarFS = "measuredItemFS"
elementVar = "measuredElement"
elementVarFS = "measuredElementFS"
valuePrefix = "Value_"
flagObsPrefix = "flagObservationStatus_"
flagMethodPrefix = "flagMethod_"


addHeadingsFCL = function(measuredItemFCL){ 
  ifelse(nchar(measuredItemFCL) == 2, 
         paste0("00",measuredItemFCL, sep = ""),
         ifelse(nchar(measuredItemFCL) == 3,
                paste0("0",measuredItemFCL, sep = ""),
                measuredItemFCL))
}


getLossFoodGroup = function(){
  # 125 primary commodities
#   lossFoodGroup = data.table(ReadDatatable(table = "loss_food_group")) %>%
#                     filter(food_general_group == "primary")


  lossFoodGroup = data.table(read.csv(file ="foodPerishableGroup.csv")) %>%
    select(FCL..Item..code.,FCL..Title,Group.Name,FBS..GROUP.Names,PERISHABLE) 
  
  setnames(lossFoodGroup, 
           old = colnames(lossFoodGroup),
           new = c("measuredItemFCL", "measuredItemNameFCL", "foodGroupName",
                    "measuredItemFBS", "foodPerishableGroup"))
  
  
  # 188 primary commodities
  distinct(lossFoodGroup,measuredItemFCL)  

  lossFoodGroup = 
  lossFoodGroup[, list(measuredItemFCL, foodGroupName, foodPerishableGroup)]
  
  ## Adding headings to FCL codes
  lossFoodGroup[, measuredItemFCL := addHeadingsFCL(measuredItemFCL)]
  
  ## Convert item FCL to numeric
  lossFoodGroup[, measuredItemFCL := as.numeric(measuredItemFCL)] 
  
  lossFoodGroup
}


getProductionData = function(){
  
  allCountries =
    GetCodeList(domain = "agriculture",
                dataset = "aproduction",
                dimension = "geographicAreaM49")[type == "country", code]
  
  
  productionKey = DatasetKey(
    domain = "agriculture",
    dataset = "aproduction",
    dimensions = list(
      Dimension(name = areaVar,
                keys = allCountries),
      Dimension(name = elementVar,
                keys = "5510"),
      Dimension(name = itemVar,
                keys = faoswsUtil::fcl2cpc(addHeadingsFCL(requiredItems))),
      Dimension(name = yearVar,
                keys = selectedYear)
    )
  )
  
    
  ## Pivot to vectorize yield computation
  productionPivot = c(
    Pivoting(code = areaVar, ascending = TRUE),
    Pivoting(code = itemVar, ascending = TRUE),
    Pivoting(code = yearVar, ascending = FALSE),
    Pivoting(code = elementVar, ascending = TRUE)
  )
  
  ## Query the data
  productionQuery = GetData(
    key = productionKey,
    flags = TRUE,
    normalized = FALSE,
    pivoting = productionPivot
  )
  
  
  ## Convert geographicAreaM49 to geographicAreaFS
  productionQuery[, geographicAreaFS := as.numeric(faoswsUtil::m492fs(as.character(geographicAreaM49)))]
  
  ## Convert measuredItemCPC to measuredItemFCL
  productionQuery[, measuredItemFCL := faoswsUtil::cpc2fcl(as.character(measuredItemCPC),returnFirst = TRUE)]
  
  
  ## Convert time to numeric
  productionQuery[, timePointYears := as.numeric(timePointYears)]
  productionQuery[, geographicAreaM49 := as.numeric(geographicAreaM49)]
  productionQuery[, measuredItemFCL := as.numeric(measuredItemFCL)] 
  
  productionQuery
  
  
  #   productionQuery%>%
  #     distinct(measuredItemCPC)
}



getImportData = function(){
  
  allCountries =
    GetCodeList(domain = "agriculture",
                dataset = "aproduction",
                dimension = "geographicAreaM49")[type == "country", code]  
  
  # Convert geographicAreaM49 to geographicAreaFS  
  allCountriesFS = faoswsUtil::m492fs(as.character(allCountries))
  # Remove "NULL"s  beacuse they are invalide codes for dimension geographicAreaFS
  allCountriesFS = na.omit(allCountriesFS) 
  # Remove codes "274" "283" "280" "281" "279"
  # because They are invalide codes for dimension geographicAreaFS
  allCountriesFS = allCountriesFS[-which(allCountriesFS == "274")]
  allCountriesFS = allCountriesFS[-which(allCountriesFS == "283")]
  allCountriesFS = allCountriesFS[-which(allCountriesFS == "280")]
  allCountriesFS = allCountriesFS[-which(allCountriesFS == "281")]
  allCountriesFS = allCountriesFS[-which(allCountriesFS == "279")]
  
  importKey = DatasetKey(
    domain = "faostat_one",
    dataset = "FS1_SUA",
    dimensions = list(
      Dimension(name = areaVarFS,
                keys = allCountriesFS),
      Dimension(name = elementVarFS,
                keys = "61"),
      Dimension(name = itemVarFS,
                keys = as.character(as.numeric(addHeadingsFCL(requiredItems)))),
      Dimension(name = yearVar,
                keys = selectedYear)
    )
  )
  
  
  ## Pivot to vectorize yield computation
  importPivot = c(
    Pivoting(code = areaVarFS, ascending = TRUE),
    Pivoting(code = itemVarFS, ascending = TRUE),
    Pivoting(code = yearVar, ascending = FALSE),
    Pivoting(code = elementVarFS, ascending = TRUE)
  )
  
  ## Query the data
  importQuery = GetData(
    key = importKey,
    flags = TRUE,
    normalized = FALSE,
    pivoting = importPivot
  )
  
  
  
  setnames(importQuery,
           old = names(importQuery),
           new = c("geographicAreaFS","measuredItemFCL","timePointYears",
                   "Value_measuredElement_5600","flagFaostat_measuredElementFS_5600")
  )
  
  
  ## Convert geographicAreaM49 to geographicAreaFS
  importQuery[, geographicAreaM49 := as.numeric(faoswsUtil::fs2m49(as.character(geographicAreaFS)))]
  
  ## Convert measuredItemCPC to measuredItemFCL
  importQuery[, measuredItemFCL := addHeadingsFCL(measuredItemFCL)]
  importQuery[, measuredItemCPC := faoswsUtil::fcl2cpc(as.character(measuredItemFCL))]
  
  
  ## Convert time to numeric
  importQuery[, timePointYears := as.numeric(timePointYears)]
  importQuery[, geographicAreaFS := as.numeric(geographicAreaFS)]
  importQuery[, measuredItemFCL := as.numeric(measuredItemFCL)] 
  
  importQuery
  
}



getSelectedLossData = function(){
  
          lossQuery = sws_query(area=1:299, 
                                item = as.numeric(lossFoodGroup$measuredItemFCL),
                                ele=121, 
                                year=1991:2015,
                                value.names = F)
          
          lossQuery = data.table(lossQuery)
          
          lossQuery = select(lossQuery, -ele)
          
          setnames(lossQuery,
                   old = names(lossQuery),
                   new = c("geographicAreaFS","measuredItemFCL","timePointYears","Value_measuredElement_5120",
                           "flagFaostat_measuredElementFS_5120"))
          
          ## Convert area FS to area M49
          lossQuery[,geographicAreaM49 := faoswsUtil::fs2m49(as.character(geographicAreaFS))]    
          
          ## Convert item FCL to area CPC
          lossQuery[,measuredItemCPC := faoswsUtil::fcl2cpc(as.character(addHeadingsFCL(measuredItemFCL)))]
          
          ## Convert time, area m49 to numeric
          lossQuery[, timePointYears := as.numeric(timePointYears)]
          lossQuery[, geographicAreaM49 := as.numeric(geographicAreaM49)]
          
          lossQuery

}

# getSelectedLossData = function(){
# 
#   allCountries =
#     GetCodeList(domain = "agriculture",
#                 dataset = "aproduction",
#                 dimension = "geographicAreaM49")[type == "country", code]
#   
#   # Convert geographicAreaM49 to geographicAreaFS  
#   allCountriesFS = faoswsUtil::m492fs(as.character(allCountries))
#   # Remove "NULL"s  beacuse they are invalide codes for dimension geographicAreaFS
#   allCountriesFS = na.omit(allCountriesFS) 
#   # Remove codes "274" "283" "280" "281" "279"
#   # because They are invalide codes for dimension geographicAreaFS
#   allCountriesFS = allCountriesFS[-which(allCountriesFS == "274")]
#   allCountriesFS = allCountriesFS[-which(allCountriesFS == "283")]
#   allCountriesFS = allCountriesFS[-which(allCountriesFS == "280")]
#   allCountriesFS = allCountriesFS[-which(allCountriesFS == "281")]
#   allCountriesFS = allCountriesFS[-which(allCountriesFS == "279")]
#   
#   lossKey = DatasetKey(
#     domain = "faostat_one",
#     dataset = "FS1_SUA",
#     dimensions = list(
#       Dimension(name = areaVarFS,
#                 keys = allCountriesFS),
#       Dimension(name = elementVarFS,
#                 keys = "121"),
#       Dimension(name = itemVarFS,
#                 keys = as.character(as.numeric(requiredItems$measuredItemFCL))),
#       Dimension(name = yearVar,
#                 keys = selectedYear)
#     )
#   )
#   
#   
#   ## Pivot to vectorize yield computation
#   lossPivot = c(
#     Pivoting(code = areaVarFS, ascending = TRUE),
#     Pivoting(code = itemVarFS, ascending = TRUE),
#     Pivoting(code = yearVar, ascending = FALSE),
#     Pivoting(code = elementVarFS, ascending = TRUE)
#   )
#   
#   ## Query the data
#   lossQuery = GetData(
#     key = lossKey,
#     flags = TRUE,
#     normalized = FALSE,
#     pivoting = lossPivot
#   )
#   
#   
#   
#   setnames(lossQuery,
#            old = names(lossQuery),
#            new = c("geographicAreaFS","measuredItemFCL","timePointYears",
#                    "Value_measuredElement_5120","flagFaostat_measuredElementFS_5120")
#   )
#   
#   
#   ## Convert geographicAreaM49 to geographicAreaFS
#   lossQuery[, geographicAreaM49 := as.numeric(faoswsUtil::fs2m49(as.character(geographicAreaFS)))]
#   
#   ## Convert measuredItemCPC to measuredItemFCL
#   lossQuery[, measuredItemFCL := addHeadingsFCL(measuredItemFCL)]
#   lossQuery[, measuredItemCPC := faoswsUtil::fcl2cpc(as.character(measuredItemFCL))]
#   
#   
#   ## Convert time to numeric
#   lossQuery[, timePointYears := as.numeric(timePointYears)]
#   
#   lossQuery[, geographicAreaFS := as.numeric(geographicAreaFS)]
#   
# 
# }

imputeLoss = function(data, lossVar, lossObservationFlagVar, lossMethodFlagVar,
                      lossModel){
  imputedData = copy(data)
  imputedData[, predicted := exp(predict(lossModel, newdata = imputedData,
                                         allow.new.levels = TRUE))]
  imputedData[(is.na(imputedData[[lossVar]]) |
                 imputedData[[lossObservationFlagVar]] %in% c("E", "I", "T")) &
                !is.na(predicted),
              `:=`(c(lossVar, lossObservationFlagVar, lossMethodFlagVar
              ),
              list(predicted, "I", "e"))]
#     imputedData[, predicted := NULL]
#     imputedData
}



mergeAllLossData = function(lossData, ...){
  explanatoryData = list(...)
  Reduce(f = function(x, y){
    keys = intersect(colnames(x), colnames(y))
    setkeyv(x, keys)
    setkeyv(y, keys)
    merge(x, y, all.x = TRUE)
  },
  x = explanatoryData, init = lossData
  )
}

removeCarryLoss = function(data, lossVar){
  data[, variance := var(.SD[[lossVar]], na.rm = TRUE),
       by = c("geographicAreaM49", "measuredItemCPC")]
  data[, duplicateValue := duplicated(.SD[[lossVar]]),
       by = c("geographicAreaM49", "measuredItemCPC")]
  data = data[!(variance == 0 & duplicateValue), ]
  data[, `:=`(c("variance", "duplicateValue"), NULL)]
  data         
}



if(updateModel){
  finalModelData = 
{
  lossFoodGroup <<- getLossFoodGroup()
  requiredItems <- unique(lossFoodGroup$measuredItemFCL)
  production <<- getProductionData()
  import <<- getImportData()
  loss <<- getSelectedLossData()%>%filter(flagFaostat_measuredElementFS_5120 == " ")
  
  #   countryTable <<-
  #     GetCodeList(domain = "agriculture",
  #                 dataset = "agriculture",
  #                 dimension = "geographicAreaM49")[type == "country",
  #                                                  list(code, description)]
  #   setnames(countryTable,
  #            old = c("code", "description"),
  #            new = c("geographicAreaM49", "geographicAreaM49Name"))
} %>%
  mergeAllLossData(lossData = loss, production, import, lossFoodGroup) %>%
  subset(x = .,
         subset = ((Value_measuredElement_5510 == 0 & Value_measuredElement_5600 > 0) |
                     (Value_measuredElement_5510 > 0 & Value_measuredElement_5600 >= 0)),
         select = c("geographicAreaM49", 
                    "measuredItemCPC", 
                    "timePointYears",
                    "Value_measuredElement_5120", # loss
                    "Value_measuredElement_5510", # production
                    "Value_measuredElement_5600", # import
                    "foodGroupName",
                    "foodPerishableGroup")) %>%
  removeCarryLoss(data = ., lossVar = "Value_measuredElement_5120") %>%
  ## Convert variables to factor
  .[, `:=`(c("geographicAreaM49",
             "measuredItemCPC", 
             "foodGroupName", 
             "foodPerishableGroup"),
           lapply(c("geographicAreaM49",
                    "measuredItemCPC", 
                    "foodGroupName", 
                    "foodPerishableGroup"),
                  FUN = function(x) as.factor(.SD[[x]])
           )
  )
  ]

lossLmeModel =
  lmer(log(Value_measuredElement_5120 + 1) ~
         -1 +
         timePointYears +
         log(Value_measuredElement_5510 + 1) + 
         (-1 + log(Value_measuredElement_5510 + 1)|
            foodPerishableGroup/foodGroupName/measuredItemCPC/geographicAreaM49)+
         log(Value_measuredElement_5600 + 1) +
         (-1 + log(Value_measuredElement_5600 + 1)|
            measuredItemCPC/geographicAreaM49),
       data = finalModelData)
}
# par(mfrow=c(1,1))
# qqnorm(residuals(lossLmeModel))
# qqline(residuals(lossLmeModel))



finalPredictData = 
{
  if(!updateModel){
    lossFoodGroup <<- getLossFoodGroup()
    requiredItems <- unique(lossFoodGroup$measuredItemFCL)
    production <<- getProductionData()
    import <<- getImportData()
    #    lossRegionClass <<- getLossRegionClass()
    #     countryTable <<-
    #       GetCodeList(domain = "agriculture",
    #                   dataset = "agriculture",
    #                   dimension = "geographicAreaM49")[type == "country",
    #                                                    list(code, description)]
    #     setnames(countryTable,
    #              old = c("code", "description"),
    #              new = c("geographicAreaM49", "geographicAreaM49Name"))
  }
  loss <<- getSelectedLossData()
} %>%
  mergeAllLossData(lossData = loss, production, import, lossFoodGroup) %>%
  subset(x = .,
         subset = ((Value_measuredElement_5510 == 0 & Value_measuredElement_5600 > 0) |
                     (Value_measuredElement_5510 > 0 & Value_measuredElement_5600 >= 0)),
         select = c("geographicAreaM49", 
                    "measuredItemCPC", 
                    "timePointYears",
                    "Value_measuredElement_5120", # loss
                    "Value_measuredElement_5510", # production
                    "Value_measuredElement_5600", # import
                    "foodGroupName",
                    "foodPerishableGroup")) %>%
  removeCarryLoss(data = ., lossVar = "Value_measuredElement_5120") %>%
  ## Convert variables to factor
  .[, `:=`(c("geographicAreaM49",
             "measuredItemCPC", 
             "foodGroupName", 
             "foodPerishableGroup"),
           lapply(c("geographicAreaM49",
                    "measuredItemCPC", 
                    "foodGroupName", 
                    "foodPerishableGroup"),
                  FUN = function(x) as.factor(.SD[[x]])
           )
  )
  ]



## Impute selected data
finalPredictDataSet =
finalPredictData %>%
  imputeLoss(data = .,
             lossVar = "Value_measuredElement_5120",
             lossObservationFlagVar =
               "flagObservationStatus_measuredElement_5120",
             lossMethodFlagVar = "flagMethod_measuredElement_5120",
             lossModel = lossLmeModel)
#   %>%
#   saveImputedLoss(data = .)

##########################################################################################
# save.image("lossImputation_ICAS_VII.RData")
rm(list=ls())
setwd("C:/Users/Golini/Dropbox/FAO/ICAS VII/")
load("lossImputation_ICAS_VII.RData")


finalModelDataSet =
  finalModelData %>%
  imputeLoss(data = .,
             lossVar = "Value_measuredElement_5120",
             lossObservationFlagVar =
               "flagObservationStatus_measuredElement_5120",
             lossMethodFlagVar = "flagMethod_measuredElement_5120",
             lossModel = lossLmeModel)

finalModelDataSet

finalModelDataSet %>%
  filter(predicted > Value_measuredElement_5600) %>%
  filter(predicted > Value_measuredElement_5510)

finalModelDataSet %>%
  filter(predicted > Value_measuredElement_5510) %>%
  filter(predicted > Value_measuredElement_5600)

finalModelDataSet[, abs_dif := abs(Value_measuredElement_5120 - round(predicted,0))]
summary(finalModelDataSet)

finalModelDataSet %>%
  select(geographicAreaM49,measuredItemCPC,timePointYears,Value_measuredElement_5120,
         predicted,dif) %>%
  filter(dif > 10000 | dif < - 10000) %>%
  filter(measuredItemCPC == "0111") 


  
finalModelDataSet[, obsRatio := round(Value_measuredElement_5120/
                                (Value_measuredElement_5510+Value_measuredElement_5600),3)]

finalModelDataSet[, predRatio := round(predicted/
                                        (Value_measuredElement_5510+Value_measuredElement_5600),3)]

finalModelDataSet[, abs_delta := abs(obsRatio - predRatio)]

shareOfficialData = 
finalModelDataSet %>%
  select(geographicAreaM49,measuredItemCPC,timePointYears,Value_measuredElement_5120,
         predicted,abs_dif,abs_delta)

summary(finalModelDataSet)

finalModelDataSet %>%
  filter(abs_delta > 0.01)


validation = function(data,lim,res){
  numNotWellPred = 
    data %>%
    filter(res > lim)
  
  numWellPred = 
    data %>%
    filter(res <= lim)
  
  shareNotWellPred = round(dim(numNotWellPred)[1]/dim(data)[1],3)
  
  shareWellPred = round(dim(numWellPred)[1]/dim(data)[1],3)
  
  return(c(shareNotWellPred,shareWellPred))
}

validation(shareOfficialData,lim = 0.05, shareOfficialData %>% select(abs_delta))
validation(shareOfficialData,lim = 8000, shareOfficialData %>% select(abs_dif))
#########################################################################################


finalPredictDataSet %>%
  filter(predicted > Value_measuredElement_5600) %>%
  filter(predicted > Value_measuredElement_5510) %>%
  select(geographicAreaM49, measuredItemCPC, timePointYears,Value_measuredElement_5120,
         Value_measuredElement_5510, Value_measuredElement_5600,predicted)


finalPredictDataSet %>%
  filter(geographicAreaM49 == 124 & measuredItemCPC == "01252") %>%
  filter(predicted > Value_measuredElement_5600) %>%
  filter(predicted > Value_measuredElement_5510)


finalPredictDataSet %>%
  filter(predicted > Value_measuredElement_5510) %>%
  filter(predicted > Value_measuredElement_5600)

finalPredictDataSet[, abs_dif := abs(Value_measuredElement_5120 - round(predicted,0))]
summary(finalPredictDataSet)

finalPredictDataSet %>%
  select(geographicAreaM49,measuredItemCPC,timePointYears,Value_measuredElement_5120,
         predicted,abs_dif) %>%
  filter(abs_dif > 10000 | abs_dif < - 10000) %>%
  filter(measuredItemCPC == "0111") 


finalPredictDataSet[, obsRatio := round(Value_measuredElement_5120/
                                        (Value_measuredElement_5510+Value_measuredElement_5600),3)]

finalPredictDataSet[, predRatio := round(predicted/
                                         (Value_measuredElement_5510+Value_measuredElement_5600),3)]

finalPredictDataSet[, abs_delta := abs(obsRatio - predRatio)]

shareOfficialData = 
  finalPredictDataSet %>%
  select(geographicAreaM49,measuredItemCPC,timePointYears,Value_measuredElement_5120,
         predicted,abs_dif,abs_delta)

summary(finalPredictDataSet)

finalPredictDataSet %>%
  filter(abs_delta > 0.01)


validation = function(data,lim,res){
  numNotWellPred = 
    data %>%
    filter(res > lim)
  
  numWellPred = 
    data %>%
    filter(res <= lim)
  
  shareNotWellPred = round(dim(numNotWellPred)[1]/dim(data)[1],3)
  
  shareWellPred = round(dim(numWellPred)[1]/dim(data)[1],3)
  
  return(c(shareNotWellPred,shareWellPred))
}

validation(shareOfficialData,lim = 0.1, shareOfficialData %>% select(abs_delta))
validation(shareOfficialData,lim = 10000, shareOfficialData %>% select(abs_dif))

#########################################################################################

finalModelDataSet %>%
  filter(geographicAreaM49 == 51 & measuredItemCPC == "0111" & timePointYears == 2000)

finalPredictDataSet %>%
  filter(geographicAreaM49 == 51 & measuredItemCPC == "0111" & timePointYears == 2000)

lossLmeModel
ranef(lossLmeModel)

exp(-0.0001044 * 2000   + (0.6930299 + 0.0003169136 + 0.0374645632 + 0.0130039846 - 0.03456254) * log(181561 + 1)
    + (0.0445586 -0.003484455 + 0.01898577) * log(375221 + 1))

# # betas for production covariate
# 51:0111:Cereals (excluding beer):non perishable                             0.0003169136
# 0111:Cereals (excluding beer):non perishable                            0.0374645632
# Cereals (excluding beer):non perishable                          0.0130039846
# non perishable                                    -0.03456254
# 
# # betas for import covariate
# 51:0111                            -3.484455e-03
# 0111                            1.898577e-02


finalPredictDataSet %>%
  filter(geographicAreaM49 == 616 & measuredItemCPC == "21170.02" & timePointYears == 2013)


exp(-0.0001044 * 2013   + (0.6930299 + 0.0297390358 -0.01675455) * log(10503.14 + 1)
    + (0.0445586) * log(293 + 1))


# # betas for production covariate
# meat:animal products                                            0.0297390358
# animal products                                   -0.01675455

```