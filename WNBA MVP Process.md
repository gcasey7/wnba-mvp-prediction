Grace Casey | [gracemkc7@gmail.com](mailto:gracemkc7@gmail.com)

WNBA MVP Prediction Model Summary  
The goal of this model was to build a model to predict the likelihood of a player winning MVP for a given season. As someone passionate about basketball and data analytics, I approached this challenge by balancing statistical rigor with basketball knowledge to craft meaningful insights. Creating this model required merging multiple basketball-related data sources, creating custom features to quantify performance, and training a predictive model using machine learning techniques. I followed a structured workflow consisting of exploratory data analysis, data cleaning, feature engineering, feature selection, model training, and MVP projections.

The first step was to understand and explore the eight different data sources provided through exploratory data analysis (EDA). I conducted two different rounds of EDA– one before and one after merging the data sets– to assess the quality, missing values, and sparsity across features. This process helped me identify key features that could influence MVP outcomes.   
	I merged all datasets into a master dataset using both the nba\_person\_id and nba\_season, accounting for players who appeared on multiple different teams in the same season due to trades. 

	During the second round of EDA, I converted the pts\_share column from a string format with percentage symbols to a float so it could be used in modeling. To account for the small fraction of WNBA players that receive MVP votes each season, I filled missing pts\_share values with 0 to represent players who did not receive votes. I also removed columns with 100% zero values and applied a 95% zero threshold, only keeping sparse features if they had strong basketball relevance (i.e. pts\_share). A correlation heat map further guided which features might be predictive.  
	  
To improve predictive power, I engineered seven custom metrics to capture the different aspects of a player's impact:

* **Net Rating Differential**: Measures how well the team performs with a player on the court versus off the court.   
* **Efficiency Per Minute:** Evaluates how productive a player is relative to their playing time. Combines assists, points, and rebounds relative to playing time.  
* **Usage-Adjusted Scoring**: Adjusts a player’s raw scoring totals based on a player’s involvement in offense (using possessions) and time played.  
* **Win Contribution:** Gives a sense of how valuable a player’s scoring is in terms of helping their team win; rewards players on winning teams.  
* **True Shooting Percentage:** Shooting efficiency accounting for field goals and free throws– utilizing 0.44 multiplier for FT because not all free throws take up a possession.  
* **Defensive Box Plus Minus (DBPM):** An estimate of a player's defensive impact by combining blocks and defensive rebounds per minute played.  
* **Total Rebound Percentage:** The percentage of total available rebounds a player collects while on the floor, normalized by minutes played.

I applied two feature selection methods: Spearman Correlation and Recursive Feature Elimination (RFE). Spearman correlation highlighted features like Efficiency Per Minute, Blocks, DBPM, Paint FG Made, and Win Contribution as highly correlated with MVP vote shares. RFE selected the top 10 features using a Random Forest model, including Paint FG Made, Points in the Paint, Opponent Points Allowed from Turnovers with the Player on Court, Win Loss Percentage, Clutch Time Seconds, and Net Rating off the Court.

I trained the model using Random Forest Regressor due to its reduced risk in overfitting, flexibility, robustness, and ability to handle non-linear relationships. The data was split into 80% training and 20% testing, excluding 2024 to prevent data leakage. The model’s performance was evaluated using Mean Squared Error (MSE) and R-squared scores. 

* **Baseline Model** (Efficiency per minute only):   
  * MSE: 0.0019  
  * R-Squared: 0.554  
* **Full Model with RFE Features**:   
  * MSE: 0.00052  
  * R-Squared: 0.7999  
* **Hyperparameter tuning using GridSearchCV further optimized the model**:  
  * MSE: 0.00057  
  * R-Squared: 0.7804

Using the optimized model, I made predictions for the 2024 WNBA season. The top predicted MVP candidates were:

| Rank | Player Name | MVP Likelihood |
| :---- | :---- | :---- |
| 1 | A’ja Wilson | 0.717339 |
| 2 | Breanna Stewart | 0.681281 |
| 3 | Napheesa Collier | 0.583213 |
| 4 | Caitlin Clark | 0.244170 |
| 5 | Brittney Griner | 0.082694 |

The model prioritizes players who not only produce elite individual stats but also contribute to team success– the type of players who typically win MVP in the WNBA. The final rankings align with consensus basketball opinion, while also identifying Napheesa Collier as an underrated MVP candidate based on her two-way impact.

Looking ahead, I would love to incorporate more defensive impact metrics, explore clustering techniques to group players by playstyle, and test different model architectures like Gradient Boosting or XGBoost.