---
title       : Pitch For Data Product
subtitle    : Estimating Prevalence of Esophageal Cancer
author      : Herpich
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Motivation

- Esophageal cancer is the eighth most common cancer globally, with nearly 450,000 net cases per year and 400,000 deaths per year

- The most common causes of esophageal cancer, both of ESCC and EAC, include smoking, alcohol, obesity, and poor diet

- Age seems to play a significant impact, as only 15% of cases are found in people younger than 55

- R contains a data frame in the datasets package based on a French case-control study for adults with esophageal cancer in Ille-et-Vilaine

--- .class #id 

## Data

- The esophageal cancer dataset has over 1,100 individual datapoints, both Cases and Controls, which are subcategorized by age group and level of alcohol and tobacco consumption



```
## [1] 25-34 35-44 45-54 55-64 65-74 75+  
## Levels: 25-34 < 35-44 < 45-54 < 55-64 < 65-74 < 75+
```

```
## [1] 0-39g/day 40-79     80-119    120+     
## Levels: 0-39g/day < 40-79 < 80-119 < 120+
```

```
## [1] 0-9g/day 10-19    20-29    30+     
## Levels: 0-9g/day < 10-19 < 20-29 < 30+
```


```r
sum(esoph$ncontrols) + sum(esoph$ncases)
```

```
## [1] 1175
```

--- .class#id

## Model

- To create a forecasting tool for esophageal cancer prevalance among sub-populations, the data was split into training and test sets, and the training data provided the input for a generalized linear model using 3-fold cross validation

- The predictor variables for this test are the interaction between age and alcohol and age and tobacco as factor variables

- The interaction between tobacco and alcohol proved not statistically significant beyond the original model

- The estimated out-of-sample average MSE was 2% (200 basis points)


```
##                   Estimate  Std. Error   t value     Pr(>|t|)
## (Intercept)   -0.040607504 0.024179005 -1.679453 9.711733e-02
## `agegp:alcgp`  0.023008633 0.002362668  9.738409 4.570201e-15
## `agegp:tobgp`  0.007825381 0.002521258  3.103760 2.672567e-03
```

--- .class#id

## Prediction Tool

- Using the linear model, age, alcohol consumption, and tobacco use can be inputted as factor variables, and the outcome will estimate approximate prevalence of Cases within the population sub-group

- Given the data, age, alcohol and tobacco use are all positive indicators for prevalence of esophageal cancer

- The tool shows the actual data in barchart form so the user can see the relative variation between actual and predicted outcomes

- It should be noted that the data is fairly incomplete, with varying numbers of people in each sub-group and often very few observations (especially in higher age groups); Additionally, it is not clear how biased the population sample is relative to the population as a whole or if there are any confounding variables altering the result, especially since typical case-control studies are self reported by subject

--- .class#id
