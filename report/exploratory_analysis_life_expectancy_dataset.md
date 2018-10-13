---
title: Exploratory analysis for life expectancy and other elements of the life table,
  Canada, all provinces except Prince Edward Island dataset
author: "Eva Y"
date: '2018-10-12'
output: 
  html_document: 
    keep_md: yes
editor_options: 
  chunk_output_type: console
---






```
## Read 81.0% of 1048950 rowsRead 1048950 rows and 17 (of 17) columns from 0.180 GB file in 00:00:03
```

## Smell Test Data

### What is the data that we have?


```
##  [1] "REF_DATE"      "GEO"           "DGUID"         "Age group"    
##  [5] "Sex"           "Element"       "UOM"           "UOM_ID"       
##  [9] "SCALAR_FACTOR" "SCALAR_ID"     "VECTOR"        "COORDINATE"   
## [13] "VALUE"         "STATUS"        "SYMBOL"        "TERMINATED"   
## [17] "DECIMALS"
```

```
## [1] 1048950      17
```

There are 17 columns and here's what I think they are. 

- REF_DATE: Between different years
- GEO: Geographic location
- DGUID: ?
- Age group: Remove 'years' and replace the x in Element with years in age group. 
- Sex: Simplify to F, M, or Both
- Element: Remove spaces in between
- UOM: ?
- UOM_ID: ?
- SCALAR_FACTOR: ?
- SCALAR_ID: ?
- VECTOR: ?
- COORDINATE: ?
- VALUE: Most important
- STATUS: ?
- SYMBOL: ?
- TERMINATED: ?
- DECIMALS: ?



### How does clean data looks like? 


```
##     REF_DATE    GEO Age_group  Sex
## 1: 1980/1982 Canada         0 Both
## 2: 1980/1982 Canada         0 Both
## 3: 1980/1982 Canada         0 Both
## 4: 1980/1982 Canada         0 Both
## 5: 1980/1982 Canada         0 Both
## 6: 1980/1982 Canada         0 Both
##                                                  Element      VALUE
## 1:                     Number of survivors at age x (lx) 1.0000e+05
## 2:           Number of deaths between age x and x+1 (dx) 9.7600e+02
## 3:          Death probability between age x and x+1 (qx) 9.7600e-03
## 4:   Margin of error of the death probability (m.e.(qx)) 1.8000e-04
## 5:    Probability of survival between age x and x+1 (px) 9.9024e-01
## 6: Number of life years lived between age x and x+1 (Lx) 9.9152e+04
##    START_YR END_YR
## 1:     1980   1982
## 2:     1980   1982
## 3:     1980   1982
## 4:     1980   1982
## 5:     1980   1982
## 6:     1980   1982
```

## Create dataset with separate years




```
##    YEAR  REF_DATE    GEO Age_group  Sex
## 1: 1980 1980/1982 Canada         0 Both
## 2: 1981 1980/1982 Canada         0 Both
## 3: 1982 1980/1982 Canada         0 Both
## 4: 1980 1980/1982 Canada         0 Both
## 5: 1981 1980/1982 Canada         0 Both
## 6: 1982 1980/1982 Canada         0 Both
##                                        Element  VALUE START_YR END_YR
## 1:           Number of survivors at age x (lx) 100000     1980   1982
## 2:           Number of survivors at age x (lx) 100000     1980   1982
## 3:           Number of survivors at age x (lx) 100000     1980   1982
## 4: Number of deaths between age x and x+1 (dx)    976     1980   1982
## 5: Number of deaths between age x and x+1 (dx)    976     1980   1982
## 6: Number of deaths between age x and x+1 (dx)    976     1980   1982
```

> How many rows and columns are there? 


```
## [1] 3146850       9
```

Number of rows is 3146850 and number of columns is 9. This seems correct since the original data has 1048950 and each interval covers three years. 

## Average duplicated years

To separate the data based on individual years, we created duplicates for years that are within the overlapping year intervals. Now, the task is to get an average for these duplicates. Let's check out how this data looks.


```
##    YEAR    GEO Age_group  Sex
## 1: 1980 Canada         0 Both
## 2: 1980 Canada         0 Both
## 3: 1980 Canada         0 Both
## 4: 1980 Canada         0 Both
## 5: 1980 Canada         0 Both
## 6: 1980 Canada         0 Both
##                                                  Element  AVG_VALUE
## 1:                     Number of survivors at age x (lx) 1.0000e+05
## 2:           Number of deaths between age x and x+1 (dx) 9.7600e+02
## 3:          Death probability between age x and x+1 (qx) 9.7600e-03
## 4:   Margin of error of the death probability (m.e.(qx)) 1.8000e-04
## 5:    Probability of survival between age x and x+1 (px) 9.9024e-01
## 6: Number of life years lived between age x and x+1 (Lx) 9.9152e+04
```



## Done 
