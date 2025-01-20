README for Quiz Performance Analysis
This project analyzes quiz performance data to provide insights on users' strengths and weaknesses in various topics. The code performs data preprocessing, feature engineering, clustering, and recommendation generation. It processes two datasets—historical and current performance data—and outputs cleaned data in new CSV files.

Steps in the Code
Step 1: Data Preprocessing
Goal: Clean and standardize the dataset by:
Stripping any leading or trailing whitespace from Quiz ID and User ID.
Converting the Topic column to lowercase for consistency.
Handling multiple concatenated topics by splitting them (e.g., "Math and Science" → ["Math", "Science"]).
Assigning an index to each unique topic for consistent reference across both datasets.
Converting Score and Accuracy columns from percentage strings (e.g., "90%") to numeric values for easier processing.
Step 2: Loading Data
Datasets:
history.csv: Contains historical quiz performance data.
current.csv: Contains current quiz performance data.
Preprocessing: Both datasets are processed using the preprocess_data() function to clean and standardize them before analysis.
Step 3: Handling Missing Values
Removal of NaN Values: Any rows with NaN values in the Score or Accuracy columns are dropped from both datasets to ensure that only complete data is used for analysis.
Step 4: Feature Engineering
Historical Data: The mean of Score and Accuracy is calculated for each topic to summarize historical performance.
Current Data: The sum of Correct Answers and Total Questions is used to calculate Accuracy_current for each topic, representing the current state of quiz performance.
The historical and current data are merged into a single DataFrame for further analysis.
Step 5: Data Normalization
Standardization: The StandardScaler is used to scale the performance data (Score, Accuracy_history, Accuracy_current, and Topic_index) to have a mean of 0 and standard deviation of 1. This normalization is crucial for clustering algorithms, as they are sensitive to the scale of input data.
Step 6: Handling Missing Data After Scaling
Imputation: Any missing values in the scaled data are filled using the SimpleImputer class with the mean strategy. This ensures there are no NaN values before clustering.
Step 7: K-Means Clustering
Clustering: The KMeans algorithm is applied to the normalized data to group quiz topics into clusters. These clusters help identify patterns in quiz performance, such as groups of topics with similar performance metrics.
Step 8: Identifying Weak and Strong Topics
Weak Topics: Topics with low Accuracy_current (< 0.5) or low Score (< 0.5) are identified as weak. These topics may need further focus and improvement.
Strong Topics: Topics with high Accuracy_current (> 0.8) and high Score (> 0.8) are considered strong. These topics indicate areas where users are performing well.
Step 9: Generating Recommendations
Weak Topics: Topics identified as weak (based on the criteria above) are recommended for improvement. These topics are extracted from the clusters and displayed for further review.
Step 10: Saving Processed Data
The cleaned and processed data is saved to new CSV files:
processed_history.csv: Contains the cleaned historical performance data.
processed_current.csv: Contains the cleaned current performance data.
These files can be used for further analysis, visualizations, or machine learning tasks.

Packages Used
The following Python packages are required to run this project. These packages perform various tasks such as data manipulation, machine learning, and data visualization.
pandas
numpy
scikit-learn
matplotlib
seaborn
