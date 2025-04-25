# wnba-mvp-prediction
Machine Learning project to predict WNBA MVPs using Random Forest

# 🏀 WNBA MVP Prediction Model

**Author:** Grace Casey | gracemkc7@gmail.com

## 📌 Project Overview
This project predicts the likelihood of a player winning the WNBA MVP award in a given season using machine learning. As a basketball fan and data analyst, I focused on merging basketball expertise with statistical modeling to identify patterns in player performance and MVP voting.

## 📊 Data & Preprocessing
- Merged 8 datasets using `nba_person_id` and `nba_season`
- Handled missing `pts_share` values and filtered features based on sparsity and relevance
- Conducted exploratory data analysis (EDA) before and after merging

## 🧠 Feature Engineering
Created 7 custom metrics to quantify player impact:
- Net Rating Differential
- Efficiency Per Minute
- Usage-Adjusted Scoring
- Win Contribution
- True Shooting %
- Defensive Box Plus Minus (DBPM)
- Total Rebound %

Used Spearman correlation and Recursive Feature Elimination (RFE) for feature selection.

## 🤖 Model Training
- Used **Random Forest Regressor** for prediction
- Training/testing split: 80/20 (2024 data excluded to prevent leakage)
- Evaluated using **Mean Squared Error (MSE)** and **R-squared**
- Best model (with RFE + GridSearchCV):  
  `MSE: 0.00057` | `R²: 0.7804`

## 🏆 2024 MVP Predictions
| Rank | Player               | MVP Likelihood |
|------|----------------------|----------------|
| 1    | A’ja Wilson          | 0.717          |
| 2    | Breanna Stewart      | 0.681          |
| 3    | Napheesa Collier     | 0.583          |
| 4    | Caitlin Clark        | 0.244          |
| 5    | Brittney Griner      | 0.083          |

## 🛠 Future Improvements
- Add more advanced defensive metrics
- Use clustering to analyze player archetypes
- Try alternative models (e.g., XGBoost, Gradient Boosting)
