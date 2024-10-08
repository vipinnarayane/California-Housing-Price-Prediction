# California Housing Price Prediction
Simplilearn: Machine Learning Project

This project leverages supervised machine learning techniques to predict housing prices in California based on various features like median income, house age, and proximity to the ocean. The dataset used is from the California Housing dataset, which includes data points such as the median house value, geographical coordinates, and other relevant attributes.

## Project Overview

The "California Housing Price Prediction" project aims to develop a machine learning model to predict median house values across various districts in California. Using data from the California Census, the project builds a predictive model that can estimate housing prices based on multiple factors, such as median income, population, and the geographical location of the district. The project also explores different regression techniques to find the most effective model for accurate predictions.

## Purpose of the Document

This document outlines the requirements and steps involved in the California Housing Price Prediction project. It serves not only to specify the functional and non-functional requirements but also to provide a clear scope of the project. The primary goal is to develop a model capable of predicting the median housing price in any district in California based on the provided features.

## Problem Statement

The project focuses on predicting the median house values in Californian districts by analyzing various features from these districts. The dataset includes information such as the population, median income, housing median age, total rooms, total bedrooms, and more. The model will learn from this data and make predictions on the median house value for any given district.

In addition, a bonus exercise involves predicting housing prices solely based on the median_income feature and visualizing the regression results.

## Project Dataset

The dataset comprises 20,640 districts or block groups, which are the smallest geographical units for which the US Census Bureau provides sample data. Each block group typically has a population ranging from 600 to 3,000 people. The dataset contains metrics such as:

- **Longitude**: A measure of how far west a house is located.
- **Latitude**: A measure of how far north a house is located.
- **Housing Median Age**: The median age of houses in the district.
- **Total Rooms**: The total number of rooms in all houses within a district.
- **Total Bedrooms**: The total number of bedrooms in all houses within a district.
- **Population**: The total population of the district.
- **Households**: The total number of households (a group of people living together) in a district.
- **Median Income**: The median income of households in the district (in tens of thousands of dollars).
- **Median House Value**: The target variable, representing the median house price in the district (in hundreds of thousands of dollars).
- **Ocean Proximity**: Categorical variable indicating the location's proximity to the ocean.

## Project Workflow
### 1. Load the Data
- **Task**: Read the "Housing.csv" file into the program and print the first few rows to understand the dataset's structure.
- **Outcome**: Extracted input features (X) and output target (y) from the dataset.

### 2. Data Preprocessing

- **Handling Missing Values**: Imputed missing values for the `total_bedrooms` feature using the mean strategy.
   - **Task**: Identify and handle missing values in the dataset.
   - **Approach**: Filled missing values with the mean of the respective column to maintain data integrity.
   - **Outcome**: Clean dataset with no missing values.
     
- **Feature Scaling**: Applied standard scaling to features with different scales to bring them into a comparable range.
   - **Standardize Data**
      - **Task**:  Standardize the features to ensure they are on a similar scale.
      - **Approach**: Applied standardization to both training and test datasets.
      - **Outcome**: Standardized data ready for model training.

- **Feature Engineering**: Created new features and applied one-hot encoding to the categorical `ocean_proximity` feature.

### 3. Exploratory Data Analysis (EDA)

- **Correlation Analysis**: Analyzed the correlation between features and the target variable (`median_house_value`).

  ![Corelation-california](https://github.com/user-attachments/assets/a8a82af7-e143-4470-8a6d-6d99d6c92bc8)

The analysis revealed 
1.	`median_income` is strongly correlated with the `median_house_value`(target attribute), people that tend to earn more money is likely to live in more expensive districts
2.	The age and the `total_rooms` in the house seems to have a positive correlation with the `median_house_value`, it make sense if the house is new a big tend to cost more
3.	We have a negative correlation between `latitude` and `median_house_value`, this means that house or districts that -ve `latitude` are less expensive.
4.	on the basis of above correlation results, the `households` , `total_bedrooms`, `ocean_proximity_ISLAND`, `population`, `longitude` are less correlated with `median_house_value` and can be excluded from feature set

- **Histogram Analysis**: Visualized the distribution of features and capped outliers for `house_median_age` and `median_house_value` to minimize their impact on the models.
 ![Histogram-california](https://github.com/user-attachments/assets/3f3f5bda-a889-4665-bb34-0a5666c7b031)

### 4.Split the Dataset

- **Task**: Divide the dataset into training and testing sets.
- **Approach**: Split the data into 80% for training and 20% for testing.
- **Outcome**: Prepared training and testing datasets for model evaluation.

### 5. Model Selection

Three models were selected and trained on the dataset to compare their performance:

#### 1. **Linear Regression**
   - **R-squared (Training)**: 0.6385162813826918
   - **R-squared (Testing)**: 0.615668886836324
   - **Root Mean Squared Error (RMSE)**: 70966.96001006386

   *Key Insight*: Linear Regression provided a baseline model with a moderate fit, but the prediction accuracy could be improved.

#### 2. **Decision Tree Regression**
   - **R-squared (Training)**: 1.0 (overfitting)
   - **R-squared (Testing)**: 0.5375808148340875
   - **Root Mean Squared Error (RMSE)**: 77843.3203269396

   *Key Insight*: The Decision Tree model showed signs of overfitting, performing well on the training data but poorly on the testing data.

#### 3. **Random Forest Regression**
   - **R-squared (Training)**: 0.9551782261502803
   - **R-squared (Testing)**: 0.7384746008843336
   - **Root Mean Squared Error (RMSE)**: 58541.03099871098

   *Key Insight*: Random Forest outperformed the other models, providing a better fit to the data with the lowest RMSE, making it the preferred model for this dataset.

### 6. Model Evaluation

The models were evaluated using R-squared and RMSE metrics:

- **R-squared**: Indicates the proportion of variance in the target variable that can be explained by the independent variables. A higher R-squared value indicates a better model fit.
- **RMSE**: Measures the average magnitude of the prediction errors. Lower RMSE values indicate better model performance.

### 7. Predict Housing Prices Using Median Income
- **Task**: Predict housing prices based on the median_income feature.
- **Approach**: Performed Linear Regression using only median_income as the independent variable and plotted the regression line.
- **Outcome**: Visual representation of the relationship between median income and housing prices, highlighting the correlation between the two.

  ![individual-plot](https://github.com/user-attachments/assets/1b939331-5cad-4d28-b12d-0c08ccbafab5)

### 8. Inference and Conclusion

- **Feature Importance**: The analysis highlighted `median_income` as the most significant predictor of housing prices. Other features like `total_rooms` and `housing_median_age` also showed positive correlations with the target variable.
- **Model Selection**: Random Forest was chosen as the final model due to its superior performance in terms of both R-squared and RMSE.
- **Key Takeaway**: The Random Forest model effectively captured the complex relationships between features and housing prices, providing more accurate predictions compared to simpler models like Linear Regression and Decision Trees.

## Future Work

- **Hyperparameter Tuning**: Further tuning of the Random Forest model could be explored to enhance performance.
- **Feature Engineering**: Additional features such as crime rates, school quality, and employment rates could be incorporated to improve the model's accuracy.
- **Geospatial Analysis**: Incorporating geospatial analysis techniques could provide deeper insights into the influence of location on housing prices.

## Repository Contents

- **Data**: The dataset used for training and testing the models.
- **Notebooks**: Jupyter notebooks containing the code for data preprocessing, EDA, model training, and evaluation.
- **Models**: Trained models and their performance metrics.
- **Reports**: Detailed analysis and findings of the project.

## References

- The California Housing Dataset (housing.csv), available through the course.
- Documentation and articles on Machine Learning Regression models.

