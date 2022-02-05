![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 4: West Nile Virus

# Research Problem

The city of Chicago has been having to deal with seasonal upticks of incidences of the West Nile virus, and it is becoming a health hazard. We have been tasked by the Chicago Department of Public Health to come up with a predictive model to identify locations where mosquitoes would have a higher chance of carrying the disease, so that resources can be effectively allocated to stop its spread.

One of the more efficient ways to prevent the disease would be to spray Zenivex, a pesticide, and by identifying the potential hotspots we can find an effective balance between preventability and cost. To this end, we will be examining the West Nile Virus dataset to train a model which can effectively predict the prevalence of the virus in certain areas.

To train a model which can predict the prevalence of the West Nile virus amongst mosquitoes within the Chicago city area, and to run a cost-benefit analysis to determine the most effective way to apply pesticides.

We will be looking at the seasonal trends of the incidences of the West Nile virus amongst mosquitoes in the Chicago city center area, and to understand the effects of weather on the prevalence of the virus. We will then examine four models (logistic regression, random forest, gradient boost classifier, and XGBoost classifier) to predict the probability of the virus being present in the even-valued years missing in our dataset. Finally, the models will be scored based on their ROC-AUC and F1 scores, and we will submit our model predictions to the [kaggle competition](https://www.kaggle.com/c/predict-west-nile-virus/overview) to be graded.

# Data Dictionary

|             Features                   | Datatype       | Description   |
|:------------------------------:|:--------------:|:-------------:|
| date                           | datetime64[ns] | The date of observation           |
| latitude                       | float64        | The latitude of the trap             |
| longitude                      | float64        | The longitude of the trap             |
| wnv_present \n (dependent variable)  | int64          | Whether the virus was present in the mosquitoes trapped             |
| tavg                           | float64        | The average temperature from both stations             |
| dew_point                      | float64        | The average dewpoint from both stations             |
| precip_total                   | float64        | The average total precipitation for both stations             |
| stn_pressure                   | float64        | The average atmospheric pressure for both stations             |
| avg_speed                      | float64        | The average wind speed for both stations             |
| year                           | float64        | The year of observation             |
| month                          | float64        | The month of observation             |
| week_of_year                   | Float64        | The week in the year of observation             |
| daylight_hours                 | float64        | The average number of hours of daylight for both stations             |
| r_humidity                     | float64        | The average relative humidity for both stations             |
| species_CULEX PIPIENS/RESTUANS | uint8          | The presence of Culex Pipens/Restuans             |
| species_CULEX RESTUANS         | uint8          | The presence of Culex Restuans             |
| species_OTHERS                 | uint8          | The presence of other mosquito species             |

# Modeling and Insights

We used 5 different models to predict the probability of the presence of mosquitoes
|                |                  Models                 |
|:--------------:|:---------------------------------------:|
| Baseline Model |               BernoulliNB               |
|     Model 1    |            Logistic Regression          |
|     Model 2    |          Random Forest Classifier       |
|     Model 3    |        Gradient Boosting Classifier     |
|     Model 4    |              XGBoost Classifier         |

The results of the models
|                |            Models            | Train AUC | Test AUC | F-score |Gridsearch AUC |
|:--------------:|:----------------------------:|:---------:|:--------:|:-------:|:---------:    |
| Baseline Model |          BernoulliNB         |   0.744   |   0.721  |  0.154  |    NA     |
|     Model 1    |      Logistic Regression     |   0.773   |   0.782  |  0.197  |   0.769   |
|     Model 2    |   Random Forest Classifier   |   0.890   |   0.817  |  0.238  |   0.832   |
|     Model 3    | Gradient Boosting Classifier |   0.891   |   0.808  |  0.249  |   0.828   |
|     Model 4    |      XGBoost Classifier      |   0.873   |   0.823  |  0.240  |   0.833   |

The best model from our testing is the Gradient Boosting Classifer model as seen from the result table between the gridsearch AUC and F-score. This could be because of the advantages of the Gradient Boosting Classifier model in which it is able to naturally handle of mixed data types, good predictive power and robustness to outliers. We chose to pick the best model by F-score because this is primarily a classification problem, and the [AUC score](https://machinelearningmastery.com/tour-of-evaluation-metrics-for-imbalanced-classification/) "can be optimistic under a severe class imbalance, especially when the number of examples in the minority class is small." Therefore, even though the kaggle competition is scored on the AUC score, we will still choose the Gradient Boost model.

For our best model of the Gradient Boosting Classifier, we obtained a public Kaggle score of 0.678 and a private Kaggle score of 0.672.

# Cost-Benefit Analysis

Given that the lifespan of the Culex species is between 2 weeks to 4 months (stated in the previous notebook), the most comprehensive spraying regime would involve spraying every 2 weeks every year at a cost of $1,015,206.

For maximum benefit, there will be no cases for WNV and we will reap $80,342 of productivity gains.

As the cost of implementing a fortnightly spray routine is much larger than the productivity gains, it is not recommended to conduct a spray routine. In addition, according to our study, spraying does not seem to have an effect on reducing the number of WNV cases in Chicago.

In notebook 1, we have also juxtaposed the number of mosquitoes trapped and the WNV cases with the weeks that spraying was conducted and observed that although the number of mosquitoes trapped decreased in 2013, the cases continued to increase even though spraying was done weekly over a 5 week period (weeks 32-36). Therefore, even if we adopt a reduced periodicity of spraying to make it more cost-effective, there is evidence that it may not be effective.

# Conclusion and Recommendations

We have built a prediction model to predict the number and locations of WNV cases in 2008, 2010, 2012 & 2014. The model does not directly help in eradicating the virus per se, but it informs us on the important features that may affect presence of the virus, which in this study are primarily weather features, which we have little to no control over.

We have also established that the desired outcome of decreasing the presence of the virus via spraying was not met as the WNV cases did not decrease after spraying and virus re-emergence was observed the following year as well. We recommend looking at other factors and solutions to control the virus.


## Recommendations

* Targeted Spraying: Instead of investing a large sum of money to conduct spraying on the entire city, better results may be obtained by focusing on larger clusters and conducting more intense spraying activities in those locations

* Change of Spray Period: From notebook 1, we notice that there is a build-up of WNV cases from week 27 - week 40 whereas spraying efforts in 2011 and 2013 happened **during** this period. A more effective solution might be to conduct spraying at week 25 (2 weeks before the build-up) to reduce mosquito activity in the following weeks

* Citizen Education: Conduct outreach and education efforts to inform citizens on the best practices to prevent mosquito breeding, periods of 'mosquito season' and the measures to prevent getting bitten

* Conduct enforcement checks
