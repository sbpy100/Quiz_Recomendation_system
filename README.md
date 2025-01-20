# Student Performance Analysis and Recommendation System

This project aims to preprocess quiz performance data, analyze historical and current performance, identify strengths and weaknesses, and recommend topics for improvement.

## Table of Contents
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Project Workflow](#project-workflow)
    - [Step 1: Import Libraries](#step-1-import-libraries)
    - [Step 2: Preprocess the Data](#step-2-preprocess-the-data)
    - [Step 3: Handle Missing Values](#step-3-handle-missing-values)
    - [Step 4: Feature Engineering](#step-4-feature-engineering)
    - [Step 5: Data Normalization](#step-5-data-normalization)
    - [Step 6: K-Means Clustering](#step-6-k-means-clustering)
    - [Step 7: Weakness and Strength Analysis](#step-7-weakness-and-strength-analysis)
    - [Step 8: Generate Recommendations](#step-8-generate-recommendations)
    - [Step 9: Visualization](#step-9-visualization)
4. [Results](#results)
5. [Future Scope](#future-scope)
6. [References](#references)

---

## Introduction
This project processes historical and current quiz data to generate insights into student performance and provides personalized recommendations based on strengths and weaknesses.

---

## Prerequisites
- Python (>= 3.6)
- Libraries: `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`

---

## Project Workflow

### Step 1: Import Libraries
Import necessary libraries like `pandas`, `numpy`, `scikit-learn`, `matplotlib`, and `seaborn` for data processing, analysis, and visualization.

---

### Step 2: Preprocess the Data
- **Clean Data**: Strip whitespaces, standardize text (lowercase), and handle missing values.
- **Handle Topics**: Split concatenated topics and assign unique indices to each topic.
- **Convert Percentages**: Transform percentage strings into numeric values.

---

### Step 3: Handle Missing Values
- Drop rows with missing values in essential columns such as `Score` and `Accuracy`.
- Use imputation techniques to handle missing data in normalized datasets.

---

### Step 4: Feature Engineering
- Aggregate historical data to calculate average `Score` and `Accuracy` per topic.
- Summarize current data to compute total `Correct Answers`, `Total Questions`, and `Accuracy` per topic.

---

### Step 5: Data Normalization
- Apply `StandardScaler` to normalize features like `Score`, `Accuracy_history`, `Accuracy_current`, and `Topic_index`.

---

### Step 6: K-Means Clustering
- Perform clustering using K-Means to categorize topics into groups based on performance metrics.
- Assign each topic to a cluster for further analysis.

---

### Step 7: Weakness and Strength Analysis
- **Weaknesses**: Identify topics with low `Score` (< 0.5) or `Accuracy_current` (< 0.5).
- **Strengths**: Identify topics with high `Score` (> 0.8) and `Accuracy_current` (> 0.8).

---

### Step 8: Generate Recommendations
- Recommend improvement areas by focusing on topics identified as weaknesses.
- Present recommendations based on clustering and performance data.

---

## Results
- Identified strong and weak topics for each student.
- Generated personalized recommendations to focus on weak topics.
- Visualized performance metrics and cluster distributions.

---

## Future Scope
- Incorporate additional features like time taken per question and difficulty levels.
- Use advanced clustering techniques like DBSCAN for better topic segmentation.
- Implement a dashboard for real-time student performance tracking.

---

