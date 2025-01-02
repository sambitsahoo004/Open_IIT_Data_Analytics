# Open_IIT_Data_Analytics
This project focuses on improving airline operational efficiency through advanced data analytics and machine learning techniques. It was developed as part of the Open IIT Data Analytics Project at IIT Kharagpur.
# OpenIIT_D42_24
## Prerequisites

Before running this notebook, ensure you have the following installed:
Python 3.x: Required to run the Jupyter Notebook.
Jupyter Notebook: To open .ipynb files interactively. Install via:

    bash

    pip install notebook

Dependencies: Install all necessary libraries by running:

    bash

    pip install -r requirements.txt

    (Note: You may need to create a requirements.txt file if one is not included, listing the libraries such as pandas, numpy, matplotlib, etc.)

Open Jupyter Notebook:

There are 3 Jupyter Notebook:
1. **EDA.ipynb**: This displays the Exploratory Data Analysis of various important features with respect to other relevant features.
2. **model.ipynb**: This notebook pre-processes the data set, removing unneccesary features, and creating new relevant features from the given features. It is trained using a model to predict flight delay.
3. **reschedule.ipynb**: In this notebook we tackle the second part of the Problem Statement which is rescheduling of flights which have been delayed by more than 15 minutes, using models to minimize overall delays. 

Start the Jupyter Notebook server by running:

    bash

        jupyter notebook

        In the Jupyter interface, navigate to the data_openiit_24.ipynb file and open it.

Run Each Cell Sequentially:
The notebook is divided into cells, each performing a specific operation.
To run a cell, select it and press Shift + Enter or use the "Run" button.
Follow any specific instructions within the notebook.

## Data Loading:
Use the data files present in the directory, which will be processed in the jupyter notebook.


## Data Preprocessing:
Here, data is cleaned and transformed to prepare it for analysis or modeling.
1. ### Import Libraries and Load Data
The required libraries (such as pandas) are imported, and the dataset is loaded into a DataFrame. This data includes columns for departure, arrival, and delay times.

2. ### Data Cleaning
   Removed irrelevant columns that won’t contribute to the analysis.
   Handled missing values, by imputation and removing rows/columns.

   Converted Date-Time Columns
   Converted date-time information to a standardized format for both departure and arrival times. This step ensures consistency and enables easier time-based calculations.

3. ### Calculate Delay Metrics
   Computed delays by subtracting scheduled times from actual times for both departures and arrivals.
   Added a new column for departure delay and arrival delay to quantify the difference in minutes.

4. ### Feature Engineering: One-Hot Encoding
   Performed one-hot encoding on categorical columns, such as ‘From’ and ‘To’ (origin and destination) and ‘Airline.’
   This converts categorical data into numerical format, making it suitable for model input.

5. ### Extract Month from Date
   Converted the ‘Used Date’ column to a datetime format.
   Extracted the month from ‘Used Date’ to create a new ‘Month’ feature for possible seasonal trend analysis.

6. ### Output Verification
   Displayed the first few rows of the DataFrame at each step to ensure transformations are correct and inspect new columns added.

## Analysis:
This section includes statistical analyses, data visualizations, or other explorations.

## Modeling:
If applicable, this section may build and train machine learning models on the processed data.
1. ### Train-Test Split:
   The data is split into training and test sets, with 80% of the data going to the training set and 20% to the test set. The target variable is Departure Delay, and the features are all other columns in df_encoded.

2. ### Feature Scaling:
   A StandardScaler is used to standardize specified numerical columns (columns_to_standardize) in x_train and x_test.
   fit_transform() is applied to the training set to calculate the mean and standard deviation and transform the data.
   transform() is applied to the test set to scale it using the training set's parameters.
   
3. ### Model Training:
A RandomForestRegressor is instantiated with a fixed random_state for reproducibility and trained on x_train and y_train using fit().

4. ### Prediction:
The model predicts y_test values using x_test, and the predictions are stored in y_pred.

5. ### Evaluation Metrics:
Mean Absolute Error (MAE): Measures the average absolute difference between the predicted and actual values, giving insight into the average prediction error in the same units as the target variable.
R² Score: Shows the proportion of variance in the target variable explained by the model; values close to 1 indicate better performance.

6. ### Results Display:
The print statements output both MAE and R² scores for easy performance interpretation

7. ### Initialize Dictionaries:
duplicate_columns: A dictionary that will store columns that have duplicates. Each key is a representative column, and its value is a list of columns that are duplicates of it.
seen_columns: A dictionary to track the unique columns encountered, using their hashed values as keys.

8. ### Iterate Over Columns:
For each column in the DataFrame:
Retrieve the current column's data.
Convert the column data to bytes. If the data type doesn’t support tobytes(), it falls back to converting the string representation of the column to bytes.

9. ### Check for Duplicates:
If the hashed value of the column data is already in seen_columns, it means that the column has a duplicate. The function then checks if this column is already recorded in duplicate_columns and updates the lists accordingly.
If the hash is not in seen_columns, it adds the column to seen_columns.

10. ### Return Duplicate Columns:
The function returns the duplicate_columns dictionary, which will contain keys for the original columns and lists of their duplicate counterparts.

## Results:
1. ### Define Range for n_estimators:
n_estimators_range is defined from 100 to 300, in increments of 20. This specifies how many trees will be in the forest.

2. ### Initialize Lists for Scores:
Train_scores and test_scores are initialized as empty lists to store the mean R² scores for each configuration of the model.

3. ### Model Training and Scoring:
A loop iterates over the specified range of n_estimators.
For each value, a RandomForestRegressor model is instantiated with that number of estimators.

4. ### Cross-Validation:
cross_val_score is used to perform 5-fold cross-validation on the training set (x_train, y_train) to calculate the mean R² score and store it in train_scores.
The same procedure is applied to the test set (x_test, y_test), storing results in test_scores.

5. ### Plotting the Results:
A plot is generated to visualize the relationship between the number of estimators and the R² scores for both training and testing datasets.
The plt.plot() function is used to create line plots for both sets of scores, with markers for clarity.
Additional plot attributes like title, labels, legend, and grid lines are added for better readability.

6. ### Random Forest Regressor Evaluation:
Explored the effect of hyperparameters (min_samples_split and min_samples_leaf) on the Random Forest model's performance using cross-validation and plot the R² scores.

7. ### Hyperparameter Tuning Preparation:
Defined a parameter grid for hyperparameter tuning using RandomizedSearchCV or GridSearchCV, though you haven't implemented the search yet.

8. ### Prediction Merging:
Predictions are merged back into the original DataFrame, which allows for easy comparisons and adjustments.

9. ### Bayesian Network Structure Learning:
Structure learning is performed using HillClimbSearch with a scoring method of BicScore, and the learned structure is printed.
A graphical representation of the learned Bayesian Network structure is plotted using networkx.

Bayesian Network Parameter Fitting:
The Bayesian Network model is initialized with the learned structure and fitted using MaximumLikelihoodEstimator.
## Troubleshooting:

ModuleNotFoundError: If you encounter an error saying a module is not found, make sure you have installed all dependencies listed in requirements.txt.
Data File Errors: Ensure that any data files used in the notebook are located in the correct directory, and that file paths in the code are correct.
