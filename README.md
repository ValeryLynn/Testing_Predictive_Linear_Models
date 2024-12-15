# Predicting drug overdose mortality rates by county level in the U.S.

This is an R project that tests four linear models to predict drug overdose mortality rates by US county level.

## Introduction
According to data collected by the Centers for Disease Control and Prevention (CDC) there were more than 63,000 drug overdose deaths in 2016. More than 66% of those involved an opioid. On October 26, 2017 the opioid crisis was officially declared a national Public Health Emergency under federal law. The economic burden of prescription opioid misuse is estimated by the CDC to be more than $78 billion a year.

County level services such as hospitals, crisis centers, and local planning boards are in need of predictive models to inform planning, preparation, and resource allocation. This model can be used to better estimate the needs of the county to address this crisis. 

Nearly half of the counties in the U.S. have missing or omitted data for drug overdose mortality in the publicly available databases. This gives an incomplete picture of the crisis at a national level, and hinders counties not reporting this data from taking preventative and curative actions. This study focuses on estimating those missing values for a more accurate (complete) visualization. Good models for prediction don’t necessarily have to provide good variable explanations. As well, collinearity does not interfere with the outcome for prediction purposes. For the scope of this project I did not conduct a test for collinearity.  In this study I put emphasis on prediction performance only. 

This study will predict missing mortality rates using social, health, and economics indicators. The purpose is to provide information that counties need to address the opioid crisis. The outcome variable in this data is a count that is Poisson distributed. When count measures are sufficiently large they can be modeled using a normal approximation and thus, a linear approach. However, at lower mean values a Poisson distribution differs from a normal distribution and therefore it is more accurate to predict using a Poisson regression. The Poisson rate model (with an offset) can be used to predict this type of data. This study will test the performance of the Poisson regression rate model in predicting missing drug mortality rates against linear regression models in an outcome variable with relatively small mean. The following models are tested:

1.	Naive Linear Regression
2.	Log-transformed Linear Regression
3.	Poisson Count Regression
4.	Poisson Rate Regression
   
## Hypothesis 
The Poisson rate regression model will better predict the outcome variable compared to a linear regression.

## Data Source
County level data of drug overdose mortality rates and social, economic, and demographic indicators are available for this model from the County Health Rankings dataset, a collaboration between the Robert Wood Johnson Foundation and the University of Wisconsin Population Health Institute. This database was built predominantly from the following:  The Behavioral Risk Factor Surveillance System (BRFSS), the National Center for Health Statistics, and the CDC WONDER mortality data.

The database for the rankings is available for downloading as an Excel spreadsheet at: 
http://www.countyhealthrankings.org/explore-health-rankings/rankings-data-documentation

Variables are all reported as percentages, rates per 100,000, ratios, or similar population adjusted measures. After data cleaning, they are all of numerical type float or integer. 

I chose to impute missing values using variable medians after an analysis of the data. The Shapiro-Wilk test was conducted on all variable to test for a normal distribution. Only one predictor variable was distributed normally.  All other variables are skewed or not normal. Therefore, the median is a more robust measure of center. 

## Method
Each model was run using all available variables. A step function was performed on the linear regression models to select for significant variables. The best linear regression model was selected based on ANOVA results. The same variables from the linear regression were used for a Poisson count regression and a Poisson rate regression. A test of prediction accuracy was conducted on these three models using Mean Absolute Percentage Error (MAPE) scores as a metric. 

## Results

|Model|	MAPE|
|-----|-----|
|Log-transformed linear regression with step selected predictors	|0.690738|
|Poisson Count Regression	|1.077028|
|Poisson Rate Regression	|0.393861|

## Conclusion
The Poisson rate regression outperformed the Poisson count regression and the log-transformed linear regression for prediction.  
