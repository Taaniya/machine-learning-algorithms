
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

 
