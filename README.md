# Predicting-loan-defaults
#### Abstract:
This task focuses on predicting loan default using data obtained from a peer-to-peer lending platform's random loan sample. The objective is to develop a model to forecast borrowers likely to default based on available features. The dataset encompasses borrower attributes, home ownerships, loan status, annual income and credit-related data. In this task, we're looking at data to see if we can predict who might not repay their loans. To do this, we split the data into two parts: one for training our models and one for testing them. This helps us make sure our models are accurate and can be trusted. Various predictive models such as ridge regression and lasso regression will be constructed and evaluated to determine the most effective model for predicting loan default.

#### Task 1:
In this task, our goal is to find the best model for predicting loan defaults using the given data. We'll do this by estimating several different models and comparing their performance. First, we'll create a new variable called "y" in the training data. This variable will be set to 1 if the "loan status" column indicates "Charged Off," and 0 otherwise. All the other columns in the dataset, except for "loan status," are considered as features or predictors. Additionally, we'll explore whether transforming certain variables, such as converting categorical ones into continuous ones, could enhance the effectiveness of our models.

#### Data Preprocessing:
First we are reading the training and test datasets from CSV files located at respective paths . Next, we are creating a new binary target variable "y" based on the "loan_status" column by the following condition, if the loan status is "Charged Off", the value of "y" is set to 1; otherwise, it is set to 0. After creating the target variable, we are dropping the "loan_status" column from both the training and test datasets since it has been transformed into the target variable. Additionally, we are dropping the "id" and "member_id" columns, likely because they are identifiers and not relevant for prediction. Then we are preprocessing the datasets by removing rows with missing values (NaN). Also, we are encoding categorical variables ('grade', 'emp_length', 'home_ownership', 'application_type') using Label Encoder to convert them into numerical format. Subsequently, we are splitting the datasets into features (X) and target variable (y) for both training and test datasets. Finally, we are computing a correlation matrix for the preprocessed training dataframe using only numeric columns and visualizing the correlation matrix as a heatmap using seaborn library, which helps in understanding the relationships between features and identifying potential multicollinearity issues.

#### Linear Regression Model:
We are creating an instance of the Linear Regression model. Then the model is trained using the training features and the corresponding target variable. The trained model is used to predict the target variable for both the training data and the test data. The MSE metric quantifies the average squared difference between the actual and predicted values and we are using this to evaluate performance. MSE is computed for both the training data predictions and the test data predictions using the actual target variable values and the predicted values.
Result: A lower MSE is better. It means our predictions are closer to the real outcomes. The MSE for the training data is about 0.0685, and for the test data, it's about 0.0690. The model performs a bit better on the training data, as its MSE is slightly lower. However, the difference between the training and test MSE is small. This suggests that our model works well on new data, not just the
data it was trained on.

#### Ridge Regression Model:
In this we are training a Ridge Regression model with cross-validated alpha selection. It fits the model to the training data, predicts target variables for both training and test data, and calculates mean squared error for the best model with the best alpha value selected by Ridge model.
Result: The "best" model exhibits an MSE of 3.917 for training and 3.825 for test data, with the best λ value being 0.08.

#### Lasso Regression Model:
This code prepares the data for Lasso Regression by scaling the features and creating a range of alpha values. It then trains the model on the scaled training data, makes predictions for both training and test data, calculates the Mean Squared Error to see how well the model performs, and selects the best alpha value that gives the most accurate predictions through cross-validation.
Result: The "best" Lasso model achieves an MSE values of 0.068 for training and for test data it’s about 0.069, with the best λ value being 0.001.

#### Random Forest Model:
This code trains a Random Forest model with 100 decision trees on the training data and predicts outcomes for both training and test data. It then calculates Mean Squared Error to evaluate how well the model performs in predicting loan defaults.
Result: The "best" Random Forest model shows an MSE values of 0.003 for training and 0.026 for test data.

#### Importance of variables in predicting:
Variables with higher importance scores are considered more influential in predicting default. In a Random Forest model, variable importance is determined based on how much each feature contributes to reducing the impurity (e.g., Gini impurity or entropy) when making decisions at each node of the decision trees in the forest. These variables have a greater impact on the model's decision-making process and are more informative for distinguishing between default and non-default cases.

#### Neural Network Model:
In this code, we are training a Multi-layer Perceptron (MLP) Regressor neural network model to predict loan defaults. The model is trained on the training data and then used to predict outcomes for both training and test datasets and evaluating the accuracy with the help of MSE.

#### Task 2:
In this code we are finding out how closely related each numeric feature is to the target variable 'y' in the preprocessed training data. It organizes these relationships and shows the 10 features that have the strongest positive and negative connections with 'y'. Positive connections mean those features tend to go up when 'y' goes up, while negative connections mean they tend to go down when 'y' goes up.
Variables correlation with “loan status”:
The correlation analysis helps us understand how numeric features relate to the chance of a loan being charged off. When a feature has a higher positive correlation, it means it's more likely to be associated with loans being charged off. On the other hand, a higher negative correlation suggests it's more likely to be linked with loans not being charged off.
Knowing these correlations helps us figure out which features are more likely to affect whether a loan is charged off or not. For instance, features that have a positive correlation with 'y’ i.e. loan status could mean they're linked to higher chances of default, while those with a negative correlation might suggest lower chances of default. This helps in picking out important features, building models, and making decisions about risk in lending.
