## Data exploration
The statistical analysis of data in the notebook includes plots that used error bars and confidence intervals.

### Error bars
* Represented graphically, indicate an uncertainty in a reported measurement and can represent one of the following statistical measures of the data - 
  1. One standard deviation 
  2. One standard error (S.E)
  3. Confidence Interval (CI)
* Error bars associated with a metric are a way to answer a statistician's question - 'How reliable my metric is?' and typically represents Standard Error or 95% confidence interval.

### Standard Error

* The measure 'Standard Error' comes into the picture when we deal with sampled data and associated metrics.
* Standard error of a metric, is the standard deviation of its sample distribution and is calculated by repeated sampling and recording of the metric (eg. mean) obtained and resulting in a distribution of this metric itself.
* Standard Error is the standard deviation of the population mean divided by the sample size.
* The Standard Error of the mesaure-sample mean is an estimate of how far from the population mean it is likely to be.
* In contrast to Standard Error, **Standard Deviation** of the sample is the degree to which individuals within a sample differ from its sample mean.

### Standard Error of the mean (SEM)

$$ \sigma_x = \frac{\sigma}{\sqrt{n}} $$

### Confidence Interval
Confidence interval is a range of values that likely will contain an unknown population parameter. 

***Confidence Level*** refers to the percentage of probability or certainty that the confidence interval would contain the true population parameter when you draw a random sample many times.

$$ CI = M \pm Z_{0.95}\sigma $$

M = Mean

$Z_{0.95}$ = No. of standard deviations extending from the mean of the normal distribution required to contain a 0.95 area.

$\sigma$ = Standard Error of the mean


## Handling missing values in Titanic dataset
* We can drop the `Cabin` column entirely due to ~77% missing data. Imputing this much data creates fake patterns.
* Because age has skewed distributions and potential outliers, fill missing `Age` values using the median (or grouped median by passenger class and sex to get more precise class medians rather than using the overall median). 
* For `Embarked`, only two rows are missing, so impute with Mode.
* For missing `Fare` entries, fill them using the median fare of that specific passenger class (`Pclass`) rather than the overall average.


References:
* https://www.kaggle.com/code/mehrdadsadeghi/titanic-ml-solution-80-accurate-on-test-data
* https://www.kaggle.com/code/reighns/titanic-a-complete-beginner-s-guide#3)-Exploratory-Data-Analysis-(EDA)-
