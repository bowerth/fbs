```
 faoswsFeed
:   

faoswsFood
:   oldToNewCommodity=ReadDatatable("food_old_code_map")

faoswsIndustrial
:   

faoswsLoss
:   

faoswsProduction
:   

faoswsSeed
:   

faoswsStandardization
:   

faoswsStock
:   

faoswsTourist
:   

faoswsTrade
:   c("hsfclmap2<-tbl_df(ReadDatatable(table=\"hsfclmap2\"))", "adjustments<-tbl_df(ReadDatatable(table=\"adjustments\"))", "tldata<-ReadDatatable(table=paste0(\"ct_tariffline_unlogged_\",year),columns=c(\"rep\",\"tyear\",\"flow\",\"comm\",\"prt\",\"weight\",\"qty\",\"qunit\",\"tvalue\",\"chapter\"),where=\"chapterIN('01','02','03','04','05','06','07','08','09','10','11','12','13','14','15','16','17','18','19','20','21','22','23','24','33','35','38','40','41','42','43','50','51','52','53')\")", "esdata<-ReadDatatable(table=paste0(\"ce_combinednomenclature_unlogged_\",year),columns=c(\"declarant\",\"partner\",\"product_nc\",\"flow\",\"period\",\"value_1k_euro\",\"qty_ton\",\"sup_quantity\"))"
) 
```

