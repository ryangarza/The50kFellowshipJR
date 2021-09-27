# The50kFellowshipJR (Ryan and Josh) 

# TO-DO BOARD 

### - Have variables named in columns 
### - Describes variables, intuition-wise, what we expect to get out of the dataset
### - *********SPLIT DATA INTO TRAINING AND TESTING**************
### - Begin initial data analysis and cleaning

## Background 
explain background of dataset and the problem at hand 

## Table of Contents 

- [Background](#Background)
- [Methodology & Approach](#Methodology-and-Approach)
- [Analysis](#Analysis)
- [Discussion](#Discussion)
- [Authors](#Authors)
- [Citations](#Citations)

## Methodology & Approach 

To approach our problem through the use of histroical data, we will analyze and interpret the initial data then use it to create statistical models using machine learning algorithms in R. This dataset comes with a response variables that we are aimed to find understanding and predictions for, which is: 

- Does an adult make more than $50,000 per year? 

 The general methodlogy we follow to working with these response variables, is the following approach: 
 
  - Data Exploration
  - Variable Selection 
  - Model Building 
  - Outcome / Conclusion

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

This dataset consists of ... (fill in) 

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Categorial variables will have an initial preprocessing data analysis of a frequency tables, proportions, missing values, and then changing strings to numbers to work with. 

```
ftable(data$variable)
prop.table(data$variable)
sum(is.na(data$variable))
data$variable = ifelse(data$variable == "string",0,1)
```

Quantative variables will have an intial preprocessing data analysis of summary statistics (mean, quartiles, missing values) and box plots. 

```
summary(data$variable)
boxplot(variable ~ response, data = data)
```

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Next we identify correlation between variables through the pearson correaltion coefficient.

The **Pearson Correlation Coefficient** measures how strong the correlation between variables might be. In mathematical terms the coefficient is denoted by r such that, 

![image](https://editor.analyticsvidhya.com/uploads/39170Formula.JPG)

Values from this equation range from [-1,1] and produce 0 when their is purely no correlation between the 2 variables and -1 and 1 when their is perfect correlation. In practice we tend to pay close attention to variables that show high correlation between eachother as we want to avoid redudancy and complexity in our models. 
The following table illustrates how to interpret the pearson correlation coeffictient.

![image](https://miro.medium.com/max/932/1*Qz_gwy4ZaSZuOpl3IyO2HA.png)

In short summary, the pearson correlation coefficient tries to draw a line fitted between the two variables and quantifies how far away the points are from the best fit line. The visualization below helps depcit this.

![image](https://editor.analyticsvidhya.com/uploads/25513Correlation.JPG)

The following code produces a matrix for the pearson correlation coefficent in our data and also a heat map visualization: 
```
library(Hmisc)
rcx=rcorr(as.matrix(data), type="pearson")
df.rcx.r=data.frame(rcx$r)
library(ggcorrplot)
ggcorrplot(rcx$r, lab = TRUE)
```
With the results of this initial data analysis, we clean and pre-remove variables from the dataset and then change route. Next, we focus on the generalized process that we follow for variable selecion through the data set. Each analysis for the respone variables will conssits of their own variable selection and feature engineering process as the data may differ in the usage different response variables (ie. each response variable is percieved as having unique solution and story). 

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The **Variable Selection** process that we use generalizes the variables into a multiple regression model which helps us understand how significant variables can be in determining the outcome (response variable). The goal of this variable selection process is to: 

- Choose the subset of predictors that is the "best" in a given sense for our machine learning models
- Avoid underfitting and overfitting our models

The formula for the multiple regression model is show below, with i potential predictors.

![image](https://miro.medium.com/max/1400/1*39FkA9sgT6E_txFT_KANjw.png)

The next question that comes to mind is specifically: How do we evaluate the potential predictors and decide the best subset?
We use 3 variable selection criterion for our models: 

-AIC (Akaike's Information Criterion)
-BIC (Bayesian Information Criterion)

Using backward and forward elimination of the variables. 


AIC and BIC scores are used as a measure of goodness of fit the quality of data used on the response variables. Below are the two formulas used to caclulate AIC and BIC.

![image](https://wikimedia.org/api/rest_v1/media/math/render/svg/fe67d436d9064a370cbe800b24b05ee8a68d491b)

![image](https://wikimedia.org/api/rest_v1/media/math/render/svg/9fb26ce833300f98a6df6039624fc7ffaf4ce7fb)

To evaluate our model to the best (lowest) Information Criterion score we use stepwise procedure of backward or forward elimination. 


## Analysis 

## Discussion

## Authors

- Ryan Garza
- Joshua Ott

## Citations 

https://archive.ics.uci.edu/ml/datasets/Adult

@misc{Dua:2019 ,
author = "Dua, Dheeru and Graff, Casey",
year = "2017",
title = "{UCI} Machine Learning Repository",
url = "http://archive.ics.uci.edu/ml",
institution = "University of California, Irvine, School of Information and Computer Sciences" }
