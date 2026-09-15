# EDA
EDA is about understanding the "story" of the data before building a model. We can follow below step-by-step process using a structured framework:

## Data Overview & Sanity Checks:
* Check the shape of the dataset (rows and columns).
* Identify data types (numerical vs. categorical).
* Preview the first few rows to understand the feature structure.

## Data Cleaning:
* Missing Values: Detect them and come up with a strategy for handling them (e.g., imputation using mean/median/mode, creating a "Missing" category, or dropping rows/columns if missingness is extreme).
* Outliers: Identify them with any of these strategies - Z-score, IQR, or box plots and decide whether to cap, transform, or remove them based on the context.
* Duplicates: Identify and remove redundant rows.

## Univariate Analysis:
* Analyze variables one by one.
* Use histograms and density plots for numerical variables to check for skewness.
* Use bar charts for categorical variables to check the frequency distribution.

## Bivariate & Multivariate Analysis:
* Look for relationships between features and the target variable (e.g., box plots of a numerical feature across different target classes).
* Use a correlation matrix (heatmap) to check for relationships between numerical features, keeping a sharp eye out for multicollinearity.


# What is a linear regression model?
* Linear regression is a fundamental supervised machine learning algorithm used to model the linear relationship between a continuous dependent variable and one or more independent variables by fitting a straight line

## Main Types:
* Simple Linear Regression: Uses a single input feature (x) to predict a target output (y).
* Multiple Linear Regression: Uses two or more input features to predict a single continuous outcome

## Assumptions:
To ensure accurate predictions, linear regression relies on four core statistical assumptions. If these assumptions are violated, the model's predictions can become unreliable or biased. You can remember these assumptions using the acronym LINE:

**1. Linearity:**
* The Concept: The relationship between the independent variables (inputs) and the dependent variable (output) must be linear.
* What it means: A straight line must be able to effectively capture the trend of the data. If the relationship is curved or exponential, linear regression will perform poorly.

**2. Independence:**
* The Concept: The observations or data points must be independent of one another.
* What it means: The value of one data point should not influence or predict the value of another. This is especially important in time-series data, where data points collected over time can be correlated with past values (known as autocorrelation).

**3. Normality (of Residuals):**
* The Concept: The errors (residuals)—which are the distances between the actual data points and the predicted regression line—must follow a normal (bell-shaped) distribution.
* What it means: While the input data itself does not need to be normally distributed, the mistakes the model makes should be centered around zero, with most errors being small and fewer errors being large.

**4. Equal Variance (Homoscedasticity):**
* The Concept: The variance of the residuals must remain constant across all levels of the independent variables.
* What it means: The spread of the data points around the regression line should look uniform. If the data points fan out or narrow down drastically as the input values increase (a condition called heteroscedasticity), the model's error estimates will be flawed.

## How It Works?
 * Best-Fit Line: The model draws a straight line (or hyperplane in higher dimensions) that minimizes the overall error or distance between the predicted values and the actual data points.
 * The Equation: It relies on the linear equation $y = mx + b$ (or $y = wx + b$), where y is the target output, x is the input feature, m (or w) is the slope, and b is the intercept.
 * Optimization: Algorithms like Ordinary Least Squares (OLS) or Gradient Descent are used to adjust the slope and intercept during training to reduce the error

### 1. Measuring Error: The Cost Function
* The most common method used to calculate error is **Mean Squared Error (MSE)**.
* **Calculate Residuals:** For every data point, the model calculates the distance between the actual value $y$ and the predicted value on the line $\hat{y}$. This distance is the error (residual).
* **Square the Errors:** The model squares each error. Squaring does two things: it removes negative signs and penalizes larger errors more heavily.
* **Average Them:** It takes the average of all these squared errors.
* The goal of the model is simple: **minimize the MSE**. The lower the cost, the better the fit.


### 2. Finding the Best Line: Optimization
* To minimize the cost function and find the optimal slope (\(w\)) and intercept (\(b\)), machine learning algorithms generally use one of two mathematical approaches:
* **Ordinary Least Squares (OLS):** This is a direct, analytical approach. It uses linear algebra and calculus to solve an exact formula that finds the absolute minimum error in one single calculation. It is highly efficient for smaller datasets.
* **Gradient Descent:** This is an iterative optimization approach used for massive datasets. The model starts with random guesses for the slope and intercept, calculates the MSE, and then takes small steps downward (in the direction of the steepest descent) until the error stops changing.


# What is multicollinearity? How does it impact linear regression?
* Multicollinearity happens when two or more independent variables in a multiple linear regression model are strongly correlated with each other, meaning they try to explain the same part of the information in the target variable.
* When you use multiple linear regression, you want each input feature to give unique, independent clues to the model.
* If two features move up and down together—like a person's height in centimeters and their height in inches—the model gets confused about which feature is actually causing the change in the target variable.


## Why Multicollinearity is a Crucial Problem
* Unstable Coefficients: Small changes in your data can cause huge, wild swings in the values of your regression coefficients.
* Unreliable p-values: It inflates the standard errors of your coefficients, making truly important variables look statistically insignificant.
* Hard to Interpret: You cannot trust the individual impact of each feature anymore because they overlap too much.

## How to Detect Multicollinearity
* Correlation Matrix: You can build a heat map or table of correlations between all pairs of input features. A correlation value close to +1 or -1 signals a red flag.
* Variance Inflation Factor (VIF):
  * This is the standard numerical test. VIF measures how much the variance of a coefficient is boosted because of collinearity.
  * A VIF value above 5 or 10 means multicollinearity is too high and needs attention.

## How to Fix Multicollinearity
* Drop a Feature: Remove one of the highly correlated variables if they provide redundant information.
* Combine Variables: Merge correlated features into a single new feature, like combining height and width into volume.
* Apply Regularization: Use advanced linear models like Ridge Regression or Lasso Regression, which shrink the coefficients and handle correlated inputs safely


## What is a p-value in linear and logistic regression models?
* In regression modeling, the p-value evaluates whether a specific independent variable has a statistically significant relationship with the target variable.
* For both linear and logistic regression, the Null Hypothesis $H_{0}$ states that an input feature has no effect on the target (meaning its mathematical weight or coefficient is zero).
* A low p-value (typically $\le$ 0.05) rejects this hypothesis, proving the feature is a statistically significant predictor.

While the core purpose is the same, how the p-value is calculated and interpreted changes based on the model type:

### 1. P-Value in Linear Regression
In linear regression, the p-value tests the straight-line relationship between a continuous input and a continuous output.
* What it tests: It determines if the slope $w$ of the feature is significantly different from zero.
* The Math: It uses a t-test. It divides the calculated coefficient by its standard error to get a t-statistic, which is then mapped to the p-value.
* Interpretation Example: If you are predicting house prices using Square Footage, a p-value of 0.002 means there is only a 0.2% chance that the relationship you see between size and price is a random coincidence. The feature is highly significant. 

### 2. P-Value in Logistic Regression
In logistic regression, the target is categorical (e.g., Yes/No, Spam/Not Spam). The model uses a curve (sigmoid function) to predict probabilities rather than straight lines.
* What it tests: It determines if a change in the input feature significantly changes the log-odds of the target event occurring.
* The Math: Instead of a t-test, it typically uses a Wald $\chi^{2}$ (Chi-Squared) test or a Z-test. This accounts for the non-linear, probabilistic nature of logistic regression.
* Interpretation Example: If you are predicting whether a patient has diabetes based on Blood Sugar, a p-value of 0.04 means Blood Sugar is a statistically significant predictor of the probability of having diabetes.


