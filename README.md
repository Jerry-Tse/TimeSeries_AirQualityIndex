# Air Quality Index: 5 Days Relative Mortality Risk
Use open source Air Quality dataset on UCI, generate reasonable Index for Air Quality, perform data analysis and make predictions.

## Table of Contents
- [Data Background](#data-background)
- [Define Air Quality Index](#define-air-quality-index)
- [Data Processing](#data-processing)
- [Data Visualization](#data-visualization)
- [Modeling and Predictions](#modeling-and-predictions)


---


## Data Background
Dataset is avaliable from [UCI website](https://archive.ics.uci.edu/ml/datasets/Air+Quality), which orginally derived from research made by De Vito, et al.(2008).  
  
Here are some hints for this datasets:  
* Data was recorded from 10.3.2004 to 04.4.2005 in an unknown city in Italy, the journal only mentioned the city as highly polluted.
* Data can be devided into PT and GT, where GT was collected from the nearby air quality monitor station, and PT was collected by the sensor right aside the road.
* Measures in GT contain unit, while PT has no unit recorded.
* GT includes CO, NOx, NO2, Bezene and NHMC(Non Metanic Hydrocarbons).
* PT includes CO, NOx, NO2, O3 and NHMC.
* All the missing value is replaced with -200.
  
## Define Air Quality Index
Generally, most Air Quality Indexes are describing how the air pollutant affect our health. Since race and ethnicity might also lead to difference resistence toward the pollutant, I narrowed down my search for reference in consider of their time and place.
  
Three reference are used to quantify the relationship between air pollutant and mortality risk:
* Michelozzi, P., et al. "Air pollution and daily mortality in Rome, Italy." Occupational and Environmental Medicine 55.9 (1998): 605-610.
* Air quality in Europe report (European environment agency, 2016)
* Chiusolo, Monica, et al. "Short-term effects of nitrogen dioxide on mortality and susceptibility factors in 10 Italian cities: the EpiAir study." Environmental health perspectives 119.9 (2011): 1233-1238.



## Data Processing
## Data Visualization
## Modeling and Predictions


