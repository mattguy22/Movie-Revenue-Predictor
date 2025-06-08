
# Movie Revenue Predictor

**Predicting Box Office Revenue Using TMDB Movie Data**

Created by Matthew Guy, Sanja Romanishan, Elizabeth Crawley, Jennifer Kim — 2025

This repository contains two main components: 
1) Movie Prediction Model: A Python-based data pipeline and regression modeling project that leverages The Movie Database (TMDB) API to collect, analyze, and predict box office revenue. This end-to-end project includes API automation, data cleaning, visual exploration, and machine learning. 
2) Movie Chatbot: A conversational agent that allows users to input variable and retrieve revenue predictions using natural language interactions.

---

## Table of Contents

- [Movie Prediction Model]
  - [Features](#features)  
  - [Installation](#installation)  
  - [Usage Instructions](#usage-instructions)  
  - [Data Collection](#data-collection)  
  - [Exploratory Visualizations](#exploratory-visualizations)  
  - [Modeling Pipeline](#modeling-pipeline)  
  - [Model Results](#model-results)  
- Movie_chatbot.ipyb
  - [Chatbot Features](#chatbot-features)
  - [Chatbot Installation](#chatbot-installation)
  - [Chatbot Usage](#chatbot-usage)
  - [Tools and Libraries](#tools-and-libraries)
- [Future Enhancements](#future-enhancements) 
- [About](#about) 
- [Resources](#resources)

---
## Movie Prediction Model
### Features

- **Automated API Calls**: Retrieves 4,000+ movies from TMDB (2000–2024) using `/discover/movie` and `/movie/{id}` endpoints.
- **Rich Movie Dataset**: For every film we retain > 30 curated attributes:
  - Basic metadata – title, release date, runtime, language
  - Financials – budget, worldwide revenue
  - Popularity metrics – TMDB popularity score, vote average & count
  - Categorical descriptors – genres, production companies, franchise status
  - Credits – director, lead actor/actress
- **EDA + Visual Insights**: Built-in Plotly visualizations for understanding trends in budget, genre, and success factors.
- **Machine Learning Integration**: Trains and compares multiple regression models to forecast box-office revenue.

---

### Installation

#### Requirements

- Python 3.10+
- Pandas, NumPy, Scikit-learn, Plotly, Requests
- Jupyter Notebook or VS Code
- TMDB API key (free at [TMDB](https://www.themoviedb.org/documentation/api))

#### Setup Steps

1. Clone/download this repo.
2. Add your API key to a `config.py` file:
   ```python
   TMDB_API_KEY = "your_api_key_here"
   ```
3. Run the notebook to extract, clean, visualize, and model data.

---

### Usage Instructions

1. Execute the notebook or script to trigger movie data collection.
2. Execute the first section to download movie data.(Tip: subsequent runs will read the cached CSV to skip the API fetch.)
3. Run EDA cells to explore trends.
4. Run modeling section to evaluate model performance.
5. Export the best model as rf_revenue_model.pkl (already scripted in the notebook) for use by the chatbot.

---

### Data Collection

- Pagination – Iterates through the first 200 API pages for each year to gather up to 20 000 IDs, then filters for complete revenue data. 
- Normalization – Flattens nested JSON (genres, production_companies) → one‑row‑per‑movie.
- Cleaning – Handles missing budgets, coerces numeric types, converts currencies to USD where necessary.  
- Stored in a single modeling-ready DataFrame

---

### Exploratory Visualizations

#### Budget vs Revenue
<img src="images/budget_revenue.png" width="600">

#### Genre Distribution
<img src="images/genre_distribution.png" width="500">

#### Popularity vs Vote Average
<img src="images/popularity_vs_rating.png" width="500">

---

## Modeling Pipeline

- **Feature Engineering**:
  -  One‑hot encode genre_ids, top‑25 directors & actors; boolean is_franchise; log‑transform revenue.
- **Data Split**: Train/test = 80/20  
- **Models Trained**:
  - Linear Regression
  - Deision Tree
  - Random Forest Regressor
- **Evaluation**:
  - MAE, RMSE, R²; cross‑validated 5‑fold on training set, final metrics on hold‑out set.

---

## Model Results
<img src="images/rf_regression.png" width="500">>

| Model               | RMSE (Millions) | R² Score |
|--------------------|------------------|----------|
| Linear Regression   | $655.4M         | -5.7+06  |
| Decision Tree       | $168.8M         | 0.62     |
| Random Forest       | $135.7M         | 0.75     |

Random Forest provides the best bias‑variance trade‑off and serves as the production model consumed by the chatbot.

### Feature Importance (Random Forest)
<img src="images/feature_importance_rf.png" width="500">

---
## Movie Chatbot
### Chatbot Features
- Natural‑Language Revenue Predictions – Users input a movie synopsis or explicit feature values (budget, genre, etc.) to receive an estimated revenue.
- What‑If Scenarios – Quickly compare how changing budget or release window affects the forecast.
- Streamlit / Voilà Front‑End – Notebook converted to a lightweight web app; no local Python knowledge required for users.
- Model API Integration – Loads the exported rf_revenue_model.pkl and preprocessing pipeline to make live predictions.

### Chatbot Installation
```
# 1. Activate the same movies environment
conda activate movies

# 2. Install Voilà & ipywidgets for notebook‑to‑web conversion
pip install voila ipywidgets

# 3. Launch the bot (runs on http://localhost:8866 by default)
voila movie_chatbot.ipynb
```

### Chatbot Usage
1) Start Voilà/Streamlit and open the served URL.
2) Enter feature values manually or paste a text prompt (e.g., “Sci‑fi film with $150 M budget, directed by Christopher Nolan, starring a top‑tier cast”).
3) Click Predict Revenue – the chatbot cleans inputs, vectorizes categorical fields, and returns:
  - Predicted worldwide revenue (USD)
  - 80 % prediction interval
  - Comparable films list (nearest‑neighbor cosine similarity on feature embeddings)

## Future Enhancements

- Add inflation adjustment to revenue
- Advanced encoding - Replace manual one‑hot with entity embeddings (genres, cast) via TensorFlow.
- Temporal Features – Incorporate release quarter & competing titles index.
- Gradient‑Boosted Models – Experiment with XGBoost & LightGBM for further gains.
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
