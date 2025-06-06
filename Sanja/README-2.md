
# 🎬 Movie Revenue Predictor

**Predicting Box Office Revenue Using TMDB Movie Data**

Created by Matthew Guy, Sanja Romanishan, Elizabeth Crawley, Jennifer Kim — 2025

A Python-based data pipeline and regression modeling project that leverages The Movie Database (TMDB) API to collect, analyze, and predict box office revenue. This end-to-end project includes API automation, data cleaning, visual exploration, and machine learning.

---

## Table of Contents

- [Features](#features)  
- [Installation](#installation)  
- [Usage Instructions](#usage-instructions)  
- [Data Collection](#data-collection)  
- [Exploratory Visualizations](#exploratory-visualizations)  
- [Modeling Pipeline](#modeling-pipeline)  
- [Model Results](#model-results)  
- [Future Enhancements](#future-enhancements)  
- [About](#about)  
- [Resources](#resources)

---

## Features

- 🔄 **Automated API Calls**: Retrieves 4,000+ movies from TMDB (2000–2024) using `/discover/movie` and `/movie/{id}` endpoints.
- 🧠 **Rich Movie Dataset**: Each record includes:
  - Title, release date, budget, revenue, runtime, genres  
  - Popularity, vote average, vote count, original language  
  - Production companies, franchise status, director, lead actor
- 📊 **EDA + Visual Insights**: Built-in visualizations for understanding trends in budget, genre, and success factors.
- 🤖 **Machine Learning Integration**: Trained regression models to predict revenue from multiple features.

---

## Installation

### Requirements

- Python 3.10+
- Pandas, NumPy, Scikit-learn, Plotly, Requests
- Jupyter Notebook or VS Code
- TMDB API key (free at [TMDB](https://www.themoviedb.org/documentation/api))

### Setup Steps

1. Clone/download this repo.
2. Add your API key to a `config.py` file:
   ```python
   TMDB_API_KEY = "your_api_key_here"
   ```
3. Run the notebook to extract, clean, visualize, and model data.

---

## Usage Instructions

1. Execute the notebook or script to trigger movie data collection.
2. A DataFrame is built with full movie metadata.
3. Run EDA cells to explore trends.
4. Run model training cells to view predictions and evaluate model performance.

---

## Data Collection

- 4,000+ movies fetched from TMDB using paginated API calls  
- Metadata includes genres, budget, revenue, actors, directors, etc.  
- Cleaned using Pandas (null handling, type conversion, flattening JSON)  
- Stored in a single modeling-ready DataFrame

---

## 📊 Exploratory Visualizations

### 🎯 Budget vs Revenue
<img src="images/budget_vs_revenue.png" width="600">

### 🎬 Genre Distribution
<img src="images/genre_distribution.png" width="500">

### 🌟 Popularity vs Vote Average
<img src="images/popularity_vs_rating.png" width="500">

---

## 🧠 Modeling Pipeline

- **Features Used**:
  - `budget`, `runtime`, `popularity`, `vote_average`, `vote_count`, genre dummies, language dummies, franchise flag
- **Target**:
  - `revenue`
- **Models Trained**:
  - Linear Regression
  - Random Forest Regressor
  - XGBoost Regressor (optional if installed)
- **Data Split**: Train/test = 80/20  
- **Preprocessing**:
  - One-hot encoding for categorical variables (genres, languages)
  - Log transformation of revenue
  - Feature scaling for numeric inputs

---

## 📈 Model Results

| Model               | RMSE (Millions) | R² Score |
|--------------------|------------------|----------|
| Linear Regression   | $158.3M          | 0.64     |
| Random Forest       | $102.6M          | 0.81     |
| XGBoost Regressor   | $97.2M           | 0.83     |

### 🔍 Feature Importance (Random Forest)
<img src="images/feature_importance_rf.png" width="500">

---

## Future Enhancements

- Add inflation adjustment to revenue
- Improve genre encoding (e.g., multi-hot vectors or embeddings)
- Add time-based features (release month, seasonal trends)
- Deploy as an interactive Streamlit app
- Train classification model to label “Box Office Hit”

---

## About

This project was developed as part of the University of Denver Data Science program. It showcases real-world API integration, data wrangling, and machine learning practices to simulate how studios might forecast revenue for upcoming films.

---

## Resources

- [TMDB API Documentation](https://developers.themoviedb.org/3)  
- Pandas, Scikit-learn, Plotly  
- DU Bootcamp Modules 11–15  
- ChatGPT — Used to debug API loops, model logic, and EDA formatting
