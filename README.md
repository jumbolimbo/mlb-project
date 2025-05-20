# MLB Trio HRR Prediction

This project predicts whether a group of **three consecutive MLB batters** will collectively go **over or under 1.5 combined Hits + Runs + RBIs (HRR)** during a game.

The model is built using **Statcast pitch-level data** and **boxscore data**, incorporating contextual features such as pitchers, batters, lineup order, pitch types, and game environment.

---

## Problem Framing

For every rolling trio of batters (e.g. 1-2-3, 2-3-4, ..., 9-1-2):
- A **binary label** is assigned:  
  - `1` if all 3 batters are over 1.5 HRR  
  - `-1` if all 3 are under 1.5 HRR  
  - `0` for mixed results

This is treated as a **3-class classification problem**.

---

## Features Used

- **Batter Identity** (encoded)
- **Pitcher Identity & Throwing Hand**
- **Pitch Type Flags** (e.g. uses curveball, slider, etc.)
- **Average Pitch Speed**
- **Number of Unique Pitch Types**
- **Home Team / Fielding Team Context**
- **Game ID / Lineup Slot (1–9)**

---

## ⚙Models Trained

-  Logistic Regression (baseline)
-  XGBoost Classifier (final)
  - ~63% test accuracy
  - Captures strong signal from player identity and velocity
  - Feature importance analyzed with `plot_importance`

---

## Files Included

| File | Description |
|------|-------------|
| `MLBACTUAL.ipynb` | Full notebook for scraping, engineering, modeling |
| `combined_data.csv` | Game-level HRR stats from boxscores |
| `df_merged.csv` | HRR data with contextual pitcher/batter information |
| `df_trios_enriched.csv` | Rolling trio dataset used for modeling |

---

## Future Directions

- Add rolling batting stats (e.g. last 7-day OPS, AVG)
- Incorporate defensive/team metrics like errors or fielding %
- Try probability-calibrated models for prop-betting use cases
- Tune class imbalance with sampling or cost-sensitive learning

---

## Author

Justin Lim  
*Data Science | Baseball Analytics Enthusiast*
