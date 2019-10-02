# Project Description

### Upgrad Pro Kabaddi League Hackathon. 

#### Objective: 
Make predictions only for the current season of the tournament, i.e., season 7.

The predictions have to be done for the following tasks - 

#### Team Analysis:
##### Task 1: Predict the winner of the tournament.
##### Task 2: Predict the top team in the points table after the completion of the league matches
##### Task 3: Predict the team with the highest points for successful raids.
##### Task 4: Predict the team with the highest points for successful tackles
##### Task 5: Predict the team with the highest super-performance total.

#### Player Analysis:
##### Task 6: Predict the player with the highest SUCCESSFUL RAID percentage.
##### Task 7: Predict the player with the highest SUCCESSFUL TACKLE percentage. 


#### Data set:
Following sites were referred to scrape the data using python BeautifulSoup library.
1. https://www.mykhel.com/kabaddi/pro-kabaddi-results/
2. https://www.prokabaddi.com/stats

The data from different pages was scraped and stored into csv files. These csv files were directly read in the Analysis using Python.

##### Data Cleaning
Missing Data was imputed with 0. The scores for different stats for the players were missing and assuming that they did not score in those areas. For example, a defender  (played 1 match) never scoring a raid point. Also a few columns had '%' in the values which were removed.

#### Approach (Steps for making Predictions):
1. Read the match results (till 01-Oct-2019), Fixtures, Players Stats as scraped from the above mentioned websites.
2. Apply Logistic Regression on the match results data set - matches that happened till 01-October-2019. 
The Winner is the target variable - the classification being 2 (team 2),1(team 1),0(draw). This model will be used to predict the result of future matches.
Raid Points, Tackle Points, All out points are independent/predictor variables.
This step produces the Model for Team Analysis.
3. FUNDAMENTAL ASSUMPTION - For future matches, the performance from last 7 (ran the model against 5-15 previous matches and probability for winners across matches was best for 7 matches) matches against each parameter (raid points, tackle points, all out points & extra points) for each team is taken and their average is used as independent variables for the future match. This observation (of averages for each of predictors) is passed to Model created as above.
4. Calculate the points accrued by each team depending upon the prediction (win/draw) by Logistic Regression model.
Get the League Winner.
    ##### Prediction: Dabang Delhi
5. Run the same Logit model for Eliminator 1 & 2, Semi Final 1 & 2, Final Match. The predictors are assumed to be average of last 7 matches.
    ##### Prediction: Dabang Delhi
6. The dataframe was updated with every match result to add up the raid points, tackle points. The final table helped determine the Team with Highest Raid Points & highest tackle points, highest super-performance total.
    ##### Team with Most Successful Raid Points : Bengal Warriors
    ##### Team with Most Successful Tackle Points : UP Yoddha
    ##### Team with highest super-performance total : Bengal Warriors
7. As per the given problem statement, SUCCESSFUL RAID percent is to be calculated as 100*(No. of Successful Raids)/(No. of Total Raids), and, SUCCESSFUL TACKLE percent is to be calculated as 100* (No. of Successful Raids)/(No. of Total Raids).
8. For predicting the Successful raid percentage, filtered the raiders & all rounders from players stats and created the data frame with success raid/tackle percentage between 0-95 (A few observations have 100 percent but they are one match-winders)
9. Dataset from season 1 to 6 will be used to train the model. Dataset for season 7 will be used to predict the highest SUCCESSFUL RAID/TACKLE percentage.
10. This is a Regression problem as the output is a continuous variable - successful raid/tackle percentage. Use various ML algorithms (Ridge, DecisionTreeRegressor, RandomForestRegressor, KNeighborsRegressor) and check the r2 score and MAE (mean absolute error) for each of those. Pick the model with highest r2 score or lowest MAE. Although tuning was not attempted. All of these were run with default parameters. Good r2_score was achieved with the dataset.
11. Season 7 stats (till date) for players was used to make prediction for Player for Highest SUCCESSFUL RAID percentage & Highest SUCCESSFUL TACKLE percentage respectively.
    ##### Player with the highest SUCCESSFUL RAID percentage: Naveen Kumar
    ##### Player with the highest SUCCESSFUL TACKLE percentage: Vishal Bhardwaj

#### Improvements:
The model could be improved by combining the players and the teams and also other stats such as height/weight of players, betting scores etc.
This is a raw model attempted with default parameters on very basic ML algorithms.
Advanced models such as Gradient Boosting, XGBoosting, Neural Networks (Deep Learning) could give better results.




