# Is a Fastball or Non-fastball Coming?
Chien Yuan Chang

## Abstract
The goal of this project was to use classification models to predict whether a pitcher will pitch a fastball or a non-fastball under certain game situations for the batters to be better prepared. Max Scherzer is the example pitcher I try to predict in this project. 

I worked with the pitch-by-pitch data between 2015-2018 downloaded from [Kaggle](https://www.kaggle.com/pschale/mlb-pitch-data-20152018). The accuracy was the main metric. I used time-series split and cross-validation, did feature engineering, EDA and feature selection, and tried algorithms of the Logistic Regression, KNN, Random Forest, AdaBoost, XGBoost, Naive Bayes, Voting and Stacking. The final model was a Hard Voting model with Logistic Regression, XGBoost, AdaBoost, XGBoost with Random Forest. The accuracy of test data was 60.7% while the fastball usage was 58.0%. The precision for the fastball and the non-fastball were 62.3% and 55.6%. The accuracy of test data was 60.7% while the fastball usage was 58.0%. The recall for the fastball and the non-fastball were 81.7% and 31.7%.

During the model training, I only can increase the accuracy by 0.1% each time and found that it's hard to predict since the pitcher was against the batter and needed to be unpredictable although there were still some pitching patterns. The model may need more data like the data of the batters and catchers.

## Design
The batter will only have 400 ms reaction time to look at the pitch, gauge the speed, type and location of the pitch, decide whether to swing, pick a swing pattern, and complete the swing to make the contact. A classification model to predict which pitch type a pitcher will pitch under certain game situations would enable the batter to have more time to react and increase the possibility of making contact.

## Data
The dataset downloaded from [Kaggle](https://www.kaggle.com/pschale/mlb-pitch-data-20152018) contains a total of 3,595,944 pitches between 2015 and 2019 in MLB with 66 columns after combining the csv files but I've found some columns of data were missing and incorrect in 2019. The data of 13,534 pitches by Max Scherzer between 2015 and 2018 was used. I also did the web scraping to get pitch-by-pitch data of Max Scherzer 41,277 pitches from 2008 to 2021 on [Baseball Savant](https://baseballsavant.mlb.com/statcast_search) for EDA. Most features I worked with were boolean or categorical. A few feature highlights included the count of the balls, the count of the strikes, the count of the outs, the count of the pitches, the count of the runners on the bases, the pitch type and result from last pitch, the result of last plate appearance, and the batting hand.


## Algorithms

*Feature Engineering*  

* Categorical variables and continuous variables were transferred, encoded or grouped into boolean variables.
* Some result features were shifted to create new features.  
* Polynomial and basic operations were tried on some features.
* Rolling sum feature was created. 
* The features were standardized.
* The data points which missed pitch type were dropped. The final dataset contains 13,454 data points.
* Final Features:
    * Three Balls: One hot encoded from the count of the balls
    * Two Strikes: One hot encoded from the count of the strikes
    * Two Balls: One hot encoded from the count of the balls
    * Left-handed Batter: Converted from string to boolean
    * Last Pitch-Ball: Shifted and one hot encoded
    * One Strike: One hot encoded from the count of the strikes
    * First Pitch: Converted from the number of pitch to boolean
    * Last Pitch-Fast: Shifted and one hot encoded
    * From 4 innings: Converted from the number of innings to boolean
    * Last PA-Long Hit: Shifted and one hot encoded
    * Last Pitch-Contact: Shifted and One hot encoded
    * One Ball: One hot encoded from the count of the balls
    * On Third Base
    * Winning: The score of the batter minus the score of the pitcher and converted from string to boolean
    * Two Outs: One hot encoded from the count of the outs

*Models*

Logistic Regression, KNN, Random Forest, AdaBoost, XGBoost, Naive Bayes, Voting and Stacking were used before settling on the Hard Voting with with Logistic Regression, XGBoost, AdaBoost, XGBoost as the model with strongest time-series cross-validation performance.

*Model Evaluation and Selection*
  
The entire dataset of 13,454 data points was split into 80/20 train vs. holdout. Predictions on the 20% holdout were limited to the very end, so this split was only used and scores seen just once.



The metric of this project was the accuracy and the method of cross-validation was time-series split.


Algorithms|Train Data|Time-series CV
---:|---:|---:
***Hard Voting with Top 4 Algorithms***|0.621|0.620
***Stacking with Top 4 Algorithms***|0.619|0.616
***Soft Voting with Top 4 Algorithms***|0.623|0.615
XGBoost|0.624|0.618
Logistic Regression|0.618|0.616
AdaBoost|0.619|0.616
XGBoost - RF|0.613|0.613
Extra Trees|0.622|0.611
Random Forest|0.622|0.610
KNN|0.627|0.607
Naive Bayes|0.611|0.601
*Baseline (Logistic)*|0.603|0.595
*Dummy (All Fastball)*|0.587|0.586

**Holdout**  

   - Accuracy: 0.607  
   - Precision: 0.623 fastball, 0.556 non-fastball  
   - Recall: 0.817 fastball, 0.317 non-fastball 
   - Actual: 0.580 fastball, 0.420 non-fastball  
   - Predicted: 0.761 fastball, 0.239 non-fastball 

## Tools
- Python Pandas and Numpy for data clean, data restructuring, exploratory data analysis and feature engineering
- Python BeautifulSoup and Selenium for web scraping
- SQLite3 for creating database and table and importing csv into table
- Python SQLAlchemy for querying from the database into Python
- Tableau Public, Python Matplotlib and Python Seaborn for exploratory data analysis and data visualization
-  for data analysis and data visualization
- Python Scikit-learn, Statsmodels, Xgboost, and Mlxtend for classification models


## Communication
In addition to [the slides of the final presentation](final_presentation.pdf), [charts](images/), [raw data](data/), and this written description, the results of EDA were on the [Tableau Public](https://public.tableau.com/app/profile/koscew/viz/Scherzer/Last_pitch) and the findings will also be posted on [my personal blog](https://koscew.github.io/) in the future.
