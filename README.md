### Project Overview

This project analyzes YouTube Shorts data to predict whether a video will have high engagement based on its metadata. The dataset is fetched using the YouTube Data API v3, and includes the following columns:
- `videoId` – Unique ID of the video
- `title` – Video title
- `publishedAt` – Timestamp of when the video was published
- `likeCount` – Number of likes
- `commentCount` – Number of comments
- `viewCount` – Number of views
- `fetchDate` – Date the data was collected

The goal is to preprocess the data, extract meaningful features, and train a logistic regression model to classify videos as high or low engagement.

## Data Preprocessing and Feature Engineering

### 1. Datetime Conversion
- Converted `publishedAt` to datetime format.  
- Created new columns:
  - `publish_hour` – Hour of the day the video was published (0–23)  
  - `publish_day` – Day of the week (0=Monday, 6=Sunday)  

### 2. Engagement Metrics
- Calculated ratios to normalize engagement relative to views:
  - `like_ratio` = `likeCount` / `viewCount`  
  - `comment_ratio` = `commentCount` / `viewCount`  
  - `engagement_score` = (`likeCount` + `commentCount`) / `viewCount`  

### 3. Text Feature
- `title_length` – Number of words in the video title  

### 4. Target Variable
- `high_engagement` – Binary variable indicating high engagement (1) if `engagement_score` ≥ median, otherwise low engagement (0)  

### 5. Encoding & Scaling
- One-hot encoded categorical features: `publish_hour`, `publish_day`  
- Scaled numerical features: `title_length`, `like_ratio`, `comment_ratio`  

### 6. Train/Test Split
- Dataset split into training and testing sets (80% train, 20% test)  
- Saved as CSVs: `X_train.csv`, `X_test.csv`, `y_train.csv`, `y_test.csv`  

## Model Training

- **Model:** Logistic Regression (`max_iter=1000`)  
- **Training:** Fitted the model on `X_train` and `y_train`  
- **Prediction:** Made predictions on `X_test`  

## Evaluation Metrics

- **Accuracy:** 0.9444  
- **Classification Report:**  
  - Precision, Recall, F1-score calculated for both classes (high and low engagement)  
- **Confusion Matrix:**  
  - Displays true positives, false positives, true negatives, and false negatives  
