### Project Proposal of Classification project
Chien Yuan Chang
#### Question/need:
I am going to build a classification model to predict which pitch type a pitcher will pitch under certain game situations. The pitch type will be the target, and Max Scherzer who is a 14-year MLB pitcher and an eight-time MLB All-Star and has three-time Cy Young Awards, 3,000 strikeouts, two no-hitter games, and a World Series championship will be the example pitcher I am going to predict.

The baseball coaches and batters can use the prediction model to make a better batting strategy to improve their performances against a certain pitcher like Max Scherzer in this project.

>* What is the framing question of your analysis, or the purpose of the model/system you plan to build? 
>* Who benefits from exploring this question or building this model/system?

#### Data Description:
* Dataset: 
  * MLB Pitch data between 2015 and 2019 will be used.
  * Data source:
      * [Kaggle](https://www.kaggle.com/pschale/mlb-pitch-data-20152018)
  * Data size: 
      * Total 3595944 pitches between 2015 and 2019 in MLB with 66 columns if we combine the csv files but some columns of data was missing in 2019
      * The data of 16312 pitches by Max Scherzer between 2015 and 2019 will be used
  * Supplemental data:
      * Scraping the pitch data from 2008 to current of Max Scherzer which will be 41277 pitches with 14 columns on [Baseball Savant](https://baseballsavant.mlb.com/statcast_search) to complete some data in 2019
 
* An individual sample/unit (total 66 columns):

	px,pz,start\_speed,end\_speed,spin\_rate,	spin\_dir,break\_angle,break\_length,break\_y,	ax,ay,az,sz\_bot,sz\_top,type\_confidence,	vx0,vy0,vz0,x,x0,y,y0,z0,pfx\_x,pfx\_z,	nasty,zone,code,type,pitch_type,event_num,	b\_score,ab\_id,b\_count,s\_count,outs,	pitch\_num,on\_1b,on\_2b,on\_3b,batter\_id,	event,g\_id,inning,o,p\_score,p\_throws,	pitcher\_id,stand,top,attendance,away\_final\_score,	away\_team,date,elapsed\_time,home\_final\_score,	home\_team,start\_time,umpire\_1B,umpire\_2B,	umpire\_3B,umpire\_HP,venue\_name,weather,	wind,delay 

	-1.598,1.869,90.6,82.8,2704.451,235.379,	43.7,6.2,23.7,-20.321,30.518,-18.145,1.41,	3.18,2,8.004,-132.465,-5.565,177.91,-3.173,	188.32,50,5.341,-11.53,7.92,43,13,C,S,	FF,3,0,2015000632,0,0,0,1,0,0,0,434158,	Walk,201500010,1,0,0,R,453286,L,TRUE,42295,	3,nyn,4/6/15,155,1,was,4:09 PM,Tim Timmons,	Chris Segal,Todd Tichenor,Tim Welke,Nationals Park,  
	76 degrees,sunny,14 mph,Out to CF,0

* Expected characteristics/features to work with (total 18 columns):
  * pitch_type: The most probable pitch type according to a neural net classification algorithm developed by Ross Paul of MLBAM. Max Scherzer has 5 main types of pitches which are four-seam fastball, slider, changeup, curveball and cutter.  
  * type_confidence: The value of the weight at the classification algorithm’s output node corresponding to the most probable pitch type, this value is multiplied by a factor of 1.5 if the pitch is known by MLBAM to be part of the pitcher’s repertoire.
  * zone: Zone 1 to 9 are the strike zones, and zone 11 to 14 are not within the strike zone. From the catcher’s view, zone 1, 4 and 7 are inside to a right handed batter from top to the bottom, zone 3, 6 and 9 are inside to a left handed batter, and zone 2, 5 and 8 are in the middle. Zone 11, 12, 13 and14 locate outside the corners of 1, 3, 7 and 9.
  * code: The codes of the result of the pitch
  * b_count: The current number of balls on the batter
  * s_count: The current number of strikes on the batter
  * outs: The current number of outs on the inning
  * pitch_num: It's the order of the pitch on the batter. 1 indicates the first pitch on the turn batting
  * on_1b: 1 indicates there was a runner on the first base
  * on_2b: 1 indicates there was a runner on the second base
  * on_3b: 1 indicates there was a runner on the third base
  * event: The detail result of the pitch
  * inning: The current inning
  * top: 1 indicates this inning was top
  * b_score: The current score of the batter team
  * p_score: The current score of the pitcher team
  * date: The date and year of the game
  * stand: The bat side of the player
  
>* What dataset(s) do you plan to use, and how will you obtain the data?
>* What is an individual sample/unit of analysis in this project? What characteristics/features do you expect to work with?

#### Tools:
* Python BeautifulSoup and Selenium for web scraping
* Python Pandas and Numpy for data clean, data restructuring, exploratory data analysis and feature engineering
* SQLite3 for creating database and table and importing csv into table
* Python SQLAlchemy for querying from the database into Python
* Tableau Public for exploratory data analysis and data visualization
* Python Matplotlib, Seaborn and/or Plotly for data visualization
* Python Scikit-learn and/or Xgboost for classification models
* Other Python libraries or tools if needed

>* How do you intend to meet the tools requirement of the project? 
>* Are you planning in advance to need or use additional tools beyond those required?

#### MVP Goal:
* A baseline model

>* What would a minimum viable product (MVP) look like for this project?