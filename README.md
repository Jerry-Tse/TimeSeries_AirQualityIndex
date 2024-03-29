



# Project -- Air Quality Index: 5 Days Relative Mortality Risk 
**Utilize open-source air pollutant datasets, define an air quality index, perform in-depth data analysis, and perform time-series forecasting.**


<img src="https://github.com/Jerry-Tse/TimeSeries_AirQualityIndex/blob/master/Images/Daily_evolution_on_pollutant_concentration.png" alt="drawing" width="470" align='center'/>&nbsp;<img src="https://github.com/Jerry-Tse/TimeSeries_AirQualityIndex/blob/master/Images/Concentration_across_hours.png" alt="drawing" width="470" align='center'/>

**Note: Access Jupyter notebook for full analysis ([Part I](https://nbviewer.jupyter.org/github/Jerry-Tse/TimeSeries_AirQualityIndex/blob/master/Project_Air_Quality_1.ipynb) & [Part II](https://nbviewer.jupyter.org/github/Jerry-Tse/TimeSeries_AirQualityIndex/blob/master/Project_Air_Quality_2.ipynb))**

## Table of Contents
- [Data Background](#data-background)
- [Define Air Quality Index](#define-air-quality-index)
- [Data Processing](#data-processing)
- [Data Visualization](#data-visualization)
- [Modeling and Predictions](#modeling-and-predictions)
- [Conclusion](#conclusion)

---


## Data Background
Dataset is avaliable from [UCI website](https://archive.ics.uci.edu/ml/datasets/Air+Quality), which orginally derived from research made by De Vito, et al.(2008).  
  
Here are some hints for this datasets:  
* Data was recorded from 10.3.2004 to 04.4.2005 in an unknown city in Italy, the journal only mentioned the city as highly polluted.
* Data can be devided into PT and GT, where GT was collected from the nearby air quality monitor station, and PT was collected by the sensor right aside the road.
* Measures in GT contain unit, while PT has no unit recorded.
* GT includes CO, NOx, NO2, Bezene and NHMC(Non Metanic Hydrocarbons).
* PT includes CO, NOx, NO2, O3 and NHMC.
* All the missing value were replaced with -200.
  
## Define Air Quality Index
Different race and ethnicity might lead to different resistence toward the pollutant. Therefore, three reference with similar background as our data are used to quantify the relationship between air pollutant and mortality risk:
* [Michelozzi, P., et al. "Air pollution and daily mortality in Rome, Italy." Occupational and Environmental Medicine 55.9 (1998): 605-610.](https://oem.bmj.com/content/55/9/605.short)
* [Air quality in Europe report (European environment agency, 2016)](https://www.eea.europa.eu/publications/air-quality-in-europe-2016)
* [Chiusolo, Monica, et al. "Short-term effects of nitrogen dioxide on mortality and susceptibility factors in 10 Italian cities: the EpiAir study." Environmental health perspectives 119.9 (2011): 1233-1238.](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3230391/)
  
The first article investigated how Particles, SO2, NO2, CO, O3 affect on short-term(Lag 0-5 days) mortality risk in Rome from 1992 to 1995. The result shows when the analysis was restricted to the deaths occurring among residents of the central area, higher coefficients were found for particles (0.66% at lag 0) and NO2 (0.55% at lag 2). No effect of
CO, SO2, or O3 was detected. While O3 show related to the mortality for the residents in city edge.
  
The second report describes when considering the air quality, the largest health impacts and the rates of YLL(years of life lost) attributable to NO2 and O3 are found in Italy compare to other European countries.
  
The third article investigate how PM10, NO2, O3 affect on short-term(Lag 0-5 days) mortality risk in 10 metropolis from 2001 to 2005. The result shows that the concentration of NO2 and PM10 plays a bigger role compare to other air pollutant. It also quantified the relationship between mortality risk and pollutant concentration.
  
The above articles suggest that the NO2 and O3 in our data would be the main target when building our index. It is also worth noted that time period in the third article actually overlaps with our data, and since we don't have the actual place where the data was recorded, the pooling average of 10 metropolis might provide an alternative path to transfer our pollutant record into health impact.

## Data Processing
Including missing value treatments, and scaling of units. 
  
When treating missing values, I decided to take average on the same hours within five sequential days, the detailed reasons are mentioned in the .ipynb with several graphs used as basis.
  
When scaling the units of PT and GT, I took out the middle 50% data of GT and PT, sorted and drew the scatter plot to find the regression line(like the way we draw QQ-plot in statistics). The reasons why we did this is based on the truth recording situation of PT and GT, see .ipynb for detailed explanation.
  
## Data Visualization
Data exploration via hourly, daily, monthly and yearly graph.
  
I take no action to the outliers in data, which is based on the formula of 1.5 times of IQR and the property when collecting our dataset. View the Data Visualization-Daily basis for more information.
  
## Modeling and Predictions
Normally in prediction of time series, we investigate the relationship of each outcome Y in different time spot. For example, ARIMA uses auto regressive line to predict future value. In this project, I selected the lagged random forest model as my model for its great interpretability and adaptation of different X. During the step of lagging, the sequential outcome Y before the target time spot are transformed into factor X, it not only gives us chances of using strong predicting model like LGBM, XGBoost, it also enables us to get insight on which outcome Y plays the most important role in future value.

## Conclusion
- Based on visualization, I use the same hour within five sequential days to impute the missing value after preprocess.
- Scaling GT to PT with Linear regression give the results of coefficient: 0.15632704 and intercept: -121.11197
- According to visualization, we can conclude that the concentration of air pollutants are highly correlated with human activity.
- Different from the traditional time series model like ARIMA, machine learning methods provide a way to include other EXO variables into consideration.
- By using the Lagging method, it helps machine learning methods not to lose the sequential information in time series.
- The random forest show pretty good predicion accuracy with this data with RMSE = 7.78
- Large portion of RMSE are contributed within the date 2005. Feb. 28 to 2005. Mar. 02, it might because the insufficient information in the same period in 2004.
