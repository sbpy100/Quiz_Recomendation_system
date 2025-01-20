# Personalized Student Recommendations for Quiz Preparation
## Overview
This project provides a Python-based solution to analyze quiz performance and generate personalized recommendations for students to improve their preparation. By processing historical and current quiz data, this system helps identify areas of strength and weakness, offering actionable steps for improvement.

## Project Structure
1 Data Preprocessing: Clean and transform the raw data.

2.Performance Analysis: Aggregate performance data to derive meaningful metrics.

3.Clustering: Group data using K-Means clustering.
4.Weakness and Strength Analysis: Identify areas of improvement and strengths.
5.Recommendation Generation: Provide personalized suggestions based on weaknesses.
6.Visualization: Visual representation of student performance through radar charts.
Prerequisites
To run this project, ensure that you have the following installed:

Python (preferably version 3.7 or higher)
Required Packages: Use the following command to install the necessary libraries:
bash
Copy
Edit
pip install pandas numpy scikit-learn matplotlib seaborn
Datasets: Ensure you have the following CSV files:
history.csv: Historical quiz performance data.
current.csv: Most recent quiz performance data.
Data Files
1. history.csv
Contains historical quiz data, including the last 5 quizzes for each user, such as:

User ID
Quiz ID
Topic
Score
Accuracy
2. current.csv
Contains the most recent quiz performance data, including:

User ID
Quiz ID
Topic
Correct Answers
Total Questions
Steps Used in the Code
1. Data Preprocessing
The preprocess_data function is used to clean and prepare the data for analysis.

ID Cleaning: Removes extra spaces and converts both Quiz ID and User ID to lowercase.
Topic Cleaning: Converts topics to lowercase and splits concatenated topics into separate values.
Score & Accuracy Conversion: Converts percentages (e.g., "80%") to numeric values for Score and Accuracy.
Missing Data Handling: Removes rows with missing Score or Accuracy.
Example Code:
python
Copy
Edit
def preprocess_data(df):
    # Data cleaning steps (stripping, converting to lowercase, splitting topics, etc.)
    ...
    return df, index_to_topic
2. Loading Datasets
The datasets are loaded into pandas dataframes using pd.read_csv():

python
Copy
Edit
history_data = pd.read_csv("history.csv")
current_data = pd.read_csv("current.csv")
Both datasets are preprocessed using the preprocess_data function.

3. Aggregating Performance Data
Performance metrics are calculated by grouping the data based on Topic_index.

Historical Performance: The mean of Score and Accuracy is calculated for each topic.
Current Performance: The sum of Correct Answers and Total Questions is computed, and Accuracy is derived.
Example Code:
python
Copy
Edit
history_performance = history_data.groupby("Topic_index").agg({"Score": "mean", "Accuracy": "mean"}).reset_index()
current_performance = current_data.groupby("Topic_index").agg({"Correct Answers": "sum", "Total Questions": "sum"}).reset_index()
current_performance["Accuracy"] = current_performance["Correct Answers"] / current_performance["Total Questions"]
4. Combining Data
The historical and current performance data are merged into a single dataframe using the Topic_index as the key.

python
Copy
Edit
performance_data = pd.merge(history_performance, current_performance, on="Topic_index", how="outer", suffixes=("_history", "_current"))
5. Data Normalization
To standardize the data, we use StandardScaler to scale Score, Accuracy_history, and Accuracy_current:

python
Copy
Edit
scaler = StandardScaler()
performance_data_scaled = scaler.fit_transform(performance_data[["Score", "Accuracy_history", "Accuracy_current", "Topic_index"]])
6. Imputation of Missing Data
After scaling, missing values are imputed using the mean value to handle any NaN values left during the scaling process.

python
Copy
Edit
imputer = SimpleImputer(strategy="mean")
performance_data_scaled = imputer.fit_transform(performance_data_scaled)
7. K-Means Clustering
K-Means clustering is used to group the data into 3 clusters based on performance data.

python
Copy
Edit
kmeans = KMeans(n_clusters=3, random_state=42)
performance_data["Cluster"] = kmeans.fit_predict(performance_data_scaled)
8. Weakness and Strength Analysis
Weak Topics: Identified based on low accuracy or score (less than 0.5).
Strong Topics: Identified based on high accuracy and score (greater than 0.8).
python
Copy
Edit
weak_topics = performance_data[(performance_data["Accuracy_current"] < 0.5) | (performance_data["Score"] < 0.5)]["Topic_index"].tolist()
strong_topics = performance_data[(performance_data["Accuracy_current"] > 0.8) & (performance_data["Score"] > 0.8)]["Topic_index"].tolist()
9. Recommendation Generation
The recommend_topics function suggests topics for the student to focus on based on their weaknesses.

python
Copy
Edit
def recommend_topics(cluster_data, weakness_list):
    recommendations = cluster_data[cluster_data["Topic_index"].isin(weakness_list)]
    return recommendations[["Topic_index", "Accuracy_current"]]
