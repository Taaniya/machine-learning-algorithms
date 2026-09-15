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

### Further reading sources:
* [What is EDA](https://www.geeksforgeeks.org/data-analysis/what-is-exploratory-data-analysis/)
* [EDA in python](https://www.geeksforgeeks.org/data-analysis/exploratory-data-analysis-in-python/)
* [Univariate, bivariate and multi-variate data and its analysis](https://www.geeksforgeeks.org/data-analysis/univariate-bivariate-and-multivariate-data-and-its-analysis/)
* [Data analysis with box-plot](https://www.geeksforgeeks.org/data-analysis/box-plot/)


# Strategies to handle missing values
* **Mean Imputation**
  * When to use: The data is numeric and forms a bell curve or symmetrical shape.
  * Why it works: The average balances out evenly when data points cluster symmetrically around the center.
  * Example: Normal human body temperatures or standardized test scores without extreme scores. 

* **Median Imputation**
  * When to use: The data is skewed (pulled toward high or low values) or has major outliers.
  * Why it works: Extreme high or low numbers pull the mean away from the true center, but the middle value (median) stays robust and unaffected.
  * Example: Household income or property prices, where a few multi-million dollar values distort the average. 

* **Best Practice Tip**
  * Always check your data distribution with a histogram or boxplot before choosing an imputation method. Furthermore, always calculate the mean or median strictly from your training dataset to prevent data leakage into your test set. 

Reference:
* [MeanMedianImputer](https://feature-engine.trainindata.com/en/1.8.x/user_guide/imputation/MeanMedianImputer.html#meanmedianimputer)

##Detecting and handling outliers
Handling outliers in machine learning involves identifying extreme data points and deciding whether to remove, transform, or leave them based on their impact on your model.

## 1. Detect Outliers
Before handling outliers, you must find them using statistical or visual tools: 
* **Interquartile Range (IQR):** Flags points below Q₁ - 1.5 × IQR or above Q₃ + 1.5 × IQR (best for skewed data).
* **Z-Score:** Flags points that deviate more than 3 standard deviations from the mean (best for normally distributed data).
* **Visual Plots:** Box plots and scatter plots help spot extreme values quickly.
* **Machine Learning Methods:** Use unsupervised algorithms like Isolation Forest or Local Outlier Factor (LOF) for complex or high-dimensional data. 


## 2. Choose a Handling Strategy
Decide how to treat outliers based on whether they are data entry errors or rare, genuine events: 
* **Removal:** Delete rows with extreme values if they are clear errors or represent a tiny fraction (<2-3%) of your data. Avoid this if you lose too much data or if the outliers represent valuable rare events like fraud. 
* Capping and Flooring (Winsorization): Replace extreme values with a specific percentile boundary (e.g., the 5th or 95th percentile) or the nearest non-outlier value.
* **Imputation:** Convert outliers to missing values (NaN) and fill them using robust central tendencies like the median, or algorithms like k-Nearest Neighbors (KNN). 
* **Transformation:** Apply mathematical functions like logarithmic or Square Root transformations to compress the scale of right-skewed data and reduce the weight of extreme points. 
* **Use Robust Models**: Switch to algorithms that are naturally resistant to outliers, such as Tree-based models (Random Forest, Gradient Boosting), or robust regression techniques like Huber Regression.


**Why these steps matter if using Logistic Regression:**
* **Capping vs. Dropping:** Dropping rows removes valid relationships that other features might hold. Capping keeps the data point but mutes its extreme leverage on the log-odds linear boundary.
* **Feature Scaling:** Logistic Regression relies on gradient descent or coordinate descent algorithms. Scaling your variables using StandardScaler after handling outliers ensures the model converges properly and coefficients remain interpretable.

References:
* https://machinelearningmastery.com/spotting-the-exception-classical-methods-for-outlier-detection-in-data-science/
* https://www.geeksforgeeks.org/machine-learning/machine-learning-outlier/
* [How To Handle Outliers In Regression Algorithms Effectively?](https://www.youtube.com/watch?v=hj0nAJ0-3qs&t=8s)

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


# What is logistic regression?
A logistic regression model assumes a linear relationship between the continuous independent variables and the log-odds (logit) of the dependent outcome, rather than a direct linear relationship with the probability itself. [1]

## What "Linearity" Means in Logistic Regression
* In standard linear regression, you expect a straight-line relationship where a one-unit change in X results in a constant change in Y. In logistic regression, the target output is a binary category (0 or 1), and the predicted probability must stay bounded between 0 and 1.
* Because an S-shaped curve cannot be modeled with a simple straight line on the probability scale, logistic regression transforms the probability ($p$) into odds
  $\frac{p}{1-p}$, and then takes the natural logarithm to get the log-odds (or logit).
* Therefore, linearity means that:
  * The log-odds change at a constant, linear rate for every one-unit increase in the predictor variable X.
* The underlying equation inside the model remains a linear combination of features:

  $z = \beta_0 + \beta_1X_1 + \dots + \beta_nX_n\$


## How Logistic Regression Works
* Logistic regression works in two primary phases: calculating the linear score and passing it through a special shaping function to squeeze the result into a valid probability. 

### 1. The Linear Equation (Logit)
* First, the model calculates a standard linear combination of the input features and their learned weights (coefficients), exactly like linear regression:

   $z=\beta_{0} + \beta_{1}X_{1} + \beta_{2}X_{2} + \dots +\beta_{n}X_{n}$
* This value z can range from negative infinity to positive infinity (-∞ to +∞). 

### 2. The Sigmoid (Logistic) Function
* To convert that unbounded number z into a usable probability between 0 and 1, the model passes z through the sigmoid function:
   $P(Y=1) = \frac{1}{1+e^{-z}}$
* This function creates a characteristic S-shaped curve. Extremely high positive values of z approach a probability of 1.0, while extreme negative values approach 0.0.


### 3. Classification via Thresholding
* Once the model outputs a predicted probability (e.g., 0.78), you apply a decision threshold—usually 0.5. If the probability is greater than or equal to the threshold, it classifies the data point as class 1; otherwise, it classifies it as class 0


### Assumptions
A logistic regression model makes five core statistical assumptions regarding the structure of the data and the relationships between variables.
* **Binary dependent variable:** The target outcome variable must be binary or dichotomous, meaning it has only two distinct categorical values like 0 or 1, true or false, or pass or fail.
* **Linearity of log-odds:** There must be a linear relationship between any continuous independent predictor variables and the log-odds (logit transformation) of the dependent variable.
* **Independence of observations:** The data points must be completely independent of one another, meaning the choice or measurement of one observation does not influence or relate to another observation.
* **Absence of multicollinearity:** The independent predictor variables should not be strongly correlated with one another, a condition you can evaluate using the Variance Inflation Factor (VIF) to ensure individual feature stability.
* **Large sample size:** The model requires a sufficiently large sample size to perform reliable estimation, with a standard guideline of having at least 10 to 20 cases of the least frequent outcome for every predictor variable you include.
* **Low or no extreme outliers:** The dataset should be free of extreme influential data points or severe outliers that can disproportionately skew the estimated coefficients of the logistic curve.


### 4. Model Training via Maximum Likelihood Estimation (MLE)

* Logistic regression uses Binary Cross-Entropy, also known as Log Loss, as its loss function instead of Mean Squared Error.
* For a single training example, the loss (L) is defined as:

$L(y,\hat{y})=-[y\log(\hat{y})+(1-y)\log(1-\hat{y})]$

* For the entire dataset with m examples, the total cost function (J) is the average of the loss across all points:
$J=-\frac{1}{m}\sum_{i=1}^{m}[y^{(i)}\log (\hat{y}^{(i)})+(1-y^{(i)})\log (1-\hat{y}^{(i)})]$

* Where:
  * $y$ is the actual true label (0 or 1).
  * ŷ is the predicted probability that the outcome is 1 (output by the sigmoid function).


### Why It Works
* **Severe Penalties for Confidence:** If the true label is 1 and the model predicts a probability near 0, the $\log(0)$ approaches infinity, heavily penalizing the wrong prediction. 
* **Convex Shape:** Unlike Mean Squared Error, which creates a wavy, non-convex curve with multiple local minimums on logistic outputs, log loss guarantees a single global minimum. This makes optimization using gradient descent much easier

### MLE
* Unlike linear regression (which uses least-squares optimization), logistic regression finds the best-fit parameters (β coefficients) using Maximum Likelihood Estimation (MLE).
* The algorithm iteratively adjusts the weights to maximize the probability (likelihood) of the model correctly predicting the actual 0 or 1 outcomes present in the training dataset.
* Optimization routines like gradient descent are typically used under the hood to find these optimal parameters. 

References -
* [Logistic Regression (and why it's different from Linear Regression](https://youtu.be/3bvM3NyMiE0?si=pLKuqs8BrosTpDB5)
* https://www.ibm.com/think/topics/logistic-regression
* https://www.geeksforgeeks.org/machine-learning/ml-cost-function-in-logistic-regression/

  

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


