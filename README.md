# Spotify Song Popularity Predictor

## Overview

Spotify Song Popularity Predictor is a machine learning project that predicts whether a song will be popular or not based on its audio features and genre.

The project follows an end-to-end machine learning workflow, from data exploration and preprocessing to model comparison and evaluation.

## Problem Statement

Predict whether a song will be popular for artists and labels, using its audio features and genre, so that they can decide which songs to promote.

## Dataset

**Dataset:** Spotify Tracks Dataset

- Total Records: 114,000 tracks
- Total Columns: 21 (after creating the target label)
- Missing Values: 3
- Problem Type: Binary Classification

### Target Variable

Created a binary target variable named `popular` from the original `popularity` column.

- `1` – Popular (popularity >= 50)
- `0` – Not Popular (popularity < 50)

### Features Used

**Numerical Features:**
- Duration
- Danceability
- Energy
- Loudness
- Speechiness
- Acousticness
- Instrumentalness
- Liveness
- Valence
- Tempo

**Categorical Features:**
- Explicit
- Key
- Mode
- Time Signature
- Track Genre

Total: 15 input features.

## Project Workflow

### 1. Data Loading and Exploration

- Loaded the Spotify Tracks Dataset.
- Examined dataset shape, columns, and missing values.
- Removed the unnecessary `Unnamed: 0` index column.
- Created the binary target variable `popular`.

### 2. Exploratory Data Analysis (EDA)

Performed exploratory analysis to understand the target distribution and relationships between features.

Key observations:
- Approximately 3 out of 4 tracks are not popular.
- The popularity distribution has a large concentration of tracks below 50.
- Popular and non-popular tracks have overlapping feature distributions.
- Audio features alone show weak correlations with the popularity label (below 0.1).
- Energy and loudness have a strong positive correlation (0.76).
- Energy and acousticness have a strong negative correlation (-0.73).

Genre was included as an additional feature because audio features alone provide a weak signal for popularity.

### 3. Train-Test Split and Baseline

Split the dataset into:
- 80% Training Data
- 20% Testing Data

Used `random_state=42` for reproducibility.

Established a baseline using `DummyClassifier` with the `most_frequent` strategy.

**Baseline Accuracy: 74.6%**

### 4. Data Preprocessing Pipeline

Implemented preprocessing using Scikit-learn Pipeline and ColumnTransformer.

**Numerical Features:**
- SimpleImputer with median strategy.
- StandardScaler for feature scaling.

**Categorical Features:**
- SimpleImputer with most frequent strategy.
- OneHotEncoder for categorical encoding.

All preprocessing steps were fitted on training data only to prevent data leakage.

### 5. Model Comparison

Compared three classification models using 3-fold cross-validation on the training data.

| Model | CV Accuracy |
|---|---:|
| Dummy Classifier (Baseline) | 74.2% |
| Logistic Regression | 77.7% |
| Random Forest Classifier | **82.7%** |

Random Forest was selected because it achieved the highest cross-validation accuracy.

### 6. Final Model Evaluation

Evaluated the selected Random Forest model on the unseen test dataset containing 22,800 tracks.

**Test Results:**

| Metric | Score |
|---|---:|
| Accuracy | 84.1% |
| Precision | 0.78 |
| Recall | 0.52 |

The model achieved 84.1% accuracy, outperforming the baseline accuracy of 74.6%.

### 7. Limitations

- The dataset contains more non-popular tracks than popular tracks, resulting in class imbalance.
- The model identifies only 52% of actual popular tracks.
- Popularity depends on factors beyond audio characteristics, such as artist fame, marketing, and playlist placements, which are not included in the available features.
- The dataset repeats some songs across different genres, meaning the same song can appear in both training and testing sets.

## Technologies & Libraries

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- KaggleHub
- Jupyter Notebook

## Repository Structure

```text
Spotify-Song-Popularity-Predictor/
│
├── Spotify_Song_Popularity_Predictor.ipynb
├── README.md
└── requirements.txt
```

## Key Learnings

- End-to-end machine learning workflow.
- Exploratory Data Analysis.
- Handling missing values.
- Numerical scaling and categorical encoding.
- Building preprocessing pipelines.
- Preventing data leakage.
- Train-test splitting and cross-validation.
- Comparing classification algorithms.
- Evaluating models using classification metrics.

## Conclusion

This project demonstrates how machine learning can be used to predict Spotify song popularity based on audio features and genre.

Among the evaluated models, Random Forest achieved the best cross-validation accuracy of 82.7% and a test accuracy of 84.1%.

The results also highlight the limitations of using audio features alone to predict music popularity.

---

**Project Name:** Spotify Song Popularity Predictor  
**Category:** Machine Learning | Binary Classification  
**Training Program:** PSEB Artificial Intelligence Training – Module 3
