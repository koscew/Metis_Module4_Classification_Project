## Prediction of the Fastball
###### Chien Yuan Chang

The goal of this project is to build a classification model to predict whether a pitcher will pitch a fastball under certain game situations. Max Scherzer is the pitcher I am going to predict. The batters can be better prepared if they know fastball is likely coming. 

To start exploring this goal, I downloaded pitch-by-pitch data between 2015-2019 from [Kaggle](https://www.kaggle.com/pschale/mlb-pitch-data-20152018) and did the web scraping to pitch-by-pitch data of Max Scherzer from 2008 to 2021 from [Baseball Savant](https://baseballsavant.mlb.com/statcast_search). I used a logistic regression model with 10 features to build the baseline model. The accuracy was 60.3% and the accuracy of time-series cross-validation was 59.5% while the percentage of the fastball usage in the training data was 58.7% and in the time-series cross-validation was 58.6%. Below are the features and their coefficients and p-values.


Features|Coefficient|P-Value
:---|:---|:---|
Constant|0.5856|<0.001
Left Batter|0.4361|<0.001
Strike count|-0.3217|<0.001
Ball Count|0.199|<0.001
Inning|-0.0746|<0.001
On 2b|-0.1884|0.002
On 3b|-0.1338|0.119
Daytime game|0.0624|0.134
On 1b|0.0152|0.751
Outs|0.002|0.937
Top Inning|0.0026|0.948


The [Charts of EDA on Tableau Public](https://public.tableau.com/app/profile/koscew/viz/Scherzer/Game_pitch?publish=yes) shows there were more fastball when the count of the balls were two or three, the count of the strikes were less than two, no runners on second or third bases, the batters were batting left-handed, last pitch was not a fastball, the temperature was under 70 degree, and last pitch was in play.

I will continue with feature selections and feature engineering and try other models like Random Forests and Boosting to find the best model.
