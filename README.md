# Capstone-Project
TIME SERIES ANALYSIS OF PATIENT ATTENDANCE AT JUMUIA HOSPITAL


I used some libraries for my analysis and plotting.

I used tseries package
forecast package
ggplot 2 package.

The main aim of the project is to examine and forecast number of outpatients attending Jumuia friends Hospital at a particular time. We want to build a
model that best defines our data and use that model to forecast for future Attendance rate. Our study therefore shows the usefulness of statistics in the
Field of medicine. In this field of medicine statistics is also highly relied on for medicine discovery trials. In the recent years jumuia friends hospital was some time overwhelmed by number of patients that attended the facility. This was as a results of poor planning on their service delivery. Jumuia friends hospital being a private hospital, maximization of profit depends on proper planning and service delivery. Our project will help the management to have proper plans on expected number of outpatients at a particular time. Ministry of health and World Health Organization can also use the same technique to estimate the medical requirement and other resources to citizens at a particular future time.

#MOTIVATION FOR THIS STUDY
Time series analysis on learning patient attendance pattern at Jumuia Clinic will help the emergency clinic develop on service delivery. In request to accomplish expansion of profit in the medical clinic the executives ought to have a model which shows direct variation between number of patients going to the facility and asset assignment by the medical clinic to serve those patients. This will be chronicled through; estimating the quantity of wellbeing laborers to serve patients on a specic timeframe,
assessing bedding limits and other clinical assets to serve patients at a given timeframe.
<img width="2249" alt="image" src="https://user-images.githubusercontent.com/120730808/208252117-8b5ac01a-36a1-45e7-a1de-bc5b48d3cd92.png">

#HISTORY BACKGROUND OF THE SAMPLE

Sampling refers to the technique or the procedure the researcher would adopt
in selecting some units from which inferences about the population is drawn.
This study will use number of outpatient attendance(dependent variable) data
for the duration within August 2018 to November 2022(independent variable).Our
sample size was determined by availability of dataset from the hospital. Jumuia
Friends Hospital started storing their recorded in a computer system in the year
2018. For the previous years their records were stored manually(on paper), that
the reason why we were unable to get attendance for the previous years.

#Data collection and technique

The research will be based mainly on secondary data from all outpatient
clinics in Jumuia Friends Hospital. The data will be obtained from the records
found in Health Records Department in Jumuia Friends Hospital.

Statement of the problem and metrics
Poor planning on number of nurses serving patient; i.e numerous circumstances had been recorded where asset prerequisites and nursing services had been overwhelmed with number of patients seeking services from the hospital. Other time hospital would set high number of nurses and experience small number of patients.
The kind of data to be used here will be from patient attendance records. This study will use number of outpatient attendance (dependent variable) data for the duration within 2018 to November 2022 (independent variable).Our sample size was determined by availability of dataset from the hospital.
Jumuia Friends Hospital started storing their recorded in a computer system in the year 2018. For the previous year's their records were stored manually (on paper), that the reason why we were unable to get attendance for the previous years. The research will be based mainly on secondary data from all outpatient clinics in Jumuia Friends Hospital. The data will be obtained from the records found in Health Records Department in Jumuia Friends Hospital.
MAPE will be used to evaluate error metrics.



#RESEARCH QUESTION

Is patient attendance rate directly proportional to the input resources (eg nurses) allocated by the hospital mangement?
If the rate is not directly proportional I study attendance pattern and try to make them proportional by introducing model for estimation purposes.

---
title: "SURVIVAL ANALYSIS"
Code used:

output:
  word_document: default
  pdf_document: default
  html_document: default
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## R Markdown

INTRODUCTION OF MY PROJECT,
Time series analysis of patients.



```{r}
library(forecast)
library(tseries)
library(ggplot2)

data1=c(621,453,657,432,567,453,234,687,691,688,691,510,534,718,732,738,789,610,631,619,551,618,639,621,589,436,492,470,585,534,619,624,789,639,694,711,834,591,414,614,501,572,619,408,562,449,397,393,390,427,415,497,602,906,800,613,713,516,418)
data1
k=ts(data1, start = c(2018), frequency = 12)
k
autoplot(k)
 #####test for stationarity
adf.test(k)
 ###our data is stationary
acf(k)
pacf(k)
kmodel=auto.arima(k, ic="aic", trace = TRUE)
kmodel=auto.arima(k, ic="bic", trace = TRUE)
kmodel=auto.arima(k, ic="aicc", trace = TRUE)
kmodel

l=kmodel$residuals
hist(kmodel$residuals)
qplot(kmodel$residuals, geom = "histogram")



acf(ts(kmodel$residuals))
pacf(ts(kmodel$residuals))

myforecast=forecast(kmodel, level = c(95), h=20)
myforecast
plot(myforecast)

summary(myforecast)

Box.test(myforecast$resid, lag = 4, type = "Ljung-Box")
Box.test(myforecast$resid, lag = 10, type = "Ljung-Box")
Box.test(myforecast$resid, lag = 20, type = "Ljung-Box")
Box.test(myforecast$resid, lag = 30, type = "Ljung-Box")
Box.test(myforecast$resid, lag = 35, type = "Ljung-Box")

```



