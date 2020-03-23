# Regression-Is-King

## Project Description
In this project, we will be using the income dataset to answer these questions:

1. Build visualizations and plots to see how the dependent variable varies with some of the other variables, such as 'education', 'marital-status', 'occupation', etc and study other interrelationships of the variables. Use them to tell a story/stories.
2. How would you transform your categorical variables and why? Which of them would you transform? If you do not want to transform any, justify why.
3. Use a technique of your choice to eliminate some of the features. Explain your method.
4. Fit a regression model to predict whether income of an individual is more than 50k. What regression model do you use? Why? How well is your model performing?
5. Use the income dataset to regress work hours on the rest of the data. Compare the R^2 with R^2 of another model that you fit with only the significant variables. Explore some interaction terms and explain why they were of interest.
6. Regress work hours of only people who are working in Sales. Once you fit a reasonable (as per your judgement) model for this data, compare the R^2 with the ones you calculated for Question 5. Explain your findings.
You can use scikit-learn, statsmodels, or any other package of your choice. Explore the packages and play around with them to get a hang of how to use them. Always refer to the documentation and look up examples of usage.

## Findings
### Question 1

<b>Importance of job titles and education on income:</b><br>
We notice that for most occupations, the number of low-income employees greatly outweigh the number of high-income employees, except for “Exec-managerial” and “Prof-specialty” roles.<br>
Moreover, the highest number listings are for those of “HS-grad” and “Some-college” of which there is a disproportionately large number of high-income wage workers compared to low income wage workers. As the education level increases, the proportion of high to low-income wage workers improves to a point where there are more high-income wage workers than low income wage workers (“Doctorate”).
  
<b>Maybe I need to get married and old to get rich?</b><br>
Interesting to see that the chances of having a high income are much higher if you’re married and neither “Divorced” nor “Never-married”. This could be due to additional allowances or incentives to work to support a family. Nonetheless, it looks like we need to find a partner!<br>
Most of the information recorded is for early to mid-level professionals. The proportion of high-income to low-income wage workers is relatively high up to the age of roughly 60 before it goes down again (probably due to retirement). Then these retirees and other older workers may turn to lower-paid part-time roles, which would explain the higher proportion of lower-income workers over age 60.
   
<b>A closeup into the gender pay gap and racial economic inequality:</b><br>
While there is a significantly higher number of records for male workers, we notice that the proportion of high-income wages is also much higher for males, which is concerning. This could be due to multiple factors (such as gender discrimination or perhaps males assuming higher paying job titles or working longer hours).
<br>While we observed that the records collected predominantly represented the white race, it is evident that the proportion of high-income wages are significantly higher for whites. 

<b>Work hard, play hard?</b><br>
As we know most conventional jobs are 40 hours per week, which explains the high frequency in that segment. We observe that anything below that will be low paying and the odds of having higher incomes increases as “hours-per-week” increases.
<br>Interestingly, we notice that there is a significantly higher number of males who work past 50 hours; whereas, there is a higher number of women working fewer hours. This could be one explanation behind the gender pay gap.

### Question 2
Certain categorical variables that might be worth transforming include the following: 
1.	“workingclass” – Combine the “Self-emp-not-inc” and “Self-emp-inc”, because the key is to know whether a person is self-employed, not whether they are incorporated or not incorporated. Combining the “local-gov” and “state-gov” levels into one group might be appropriate, as their incomes are likely similar.  The “Federal-gov” level may need to remain separate as these jobs are oft considered more elite than state and local government jobs.

2.	“marital-status” – Combine “Married-AF-spouse” and “Married-civ-spouse”, because the key is to know whether a person is married, not whether their spouse is in the Armed Forces or is a civilian. Keeping “Married-spouse-absent” by itself might be appropriate as that may have an affect on whether the person makes more or less than $50k. Also, combining “Divorced”, “Never-married”, “Separated”, and “Widowed” into “Not married” also seems appropriate. The key here is that the person does not have partner with whom they have combined income, so this may affect whether they make more or less than $50k.

3.	“native-country” – Combine the 42 countries (approximately) into larger regions such as “North America”, “Europe”, “Asia”. This likely will not lose any information, but will simplify the number of levels involved.

### Question 3
With the Y-variable as “income_ >50k”, we eliminated certain variables by finding correlations between all the variables with all the other variables. Then we focused on just the correlations between all the variables and the variable “income_ >50k”. The following variables had high correlations with the variable “income_ >50k”, so were kept:

Age, education-num, marital-status_Married, marital-status_Never-married, marital-status_Widowed, capital-gain, relationship_ Husband
relationship_ Not-in-family, relationship_ Other-relative, 
relationship_ Own-child, relationship_ Unmarried, hours-per-week.

All the other variables had low correlations with the variable “income_ >50k”, so they were eliminated. See the output of   in the code to see the correlations listed from largest to smallest. (The output is too large to fit in this document.)

### Question 4
The goal here is to predict the whether the income of an individual is more than 50k. The regression model that we have used in this case is logistic regression. Logistic regression is generally used when the dependent variable is dichotomous. Since we are trying to predict binary answer for the question here, logic regression is used.
We picked significant predictors by evaluating their correlation with the dependent variable.
To evaluate the model, we have used train and test dataset (out-of-sample testing) with a 70-30 split. We fit the model using the train dataset and got the metrics such as precision, F1 score using predicted values for the test dataset. We have a model with an accuracy of 84%. The precision and recall are 0.83 and 0.84 (weighted average). Refer to Part 1 of Appendix for the model scores and ROC graph.

### Question 5
The R-squared for the full model is very low at 0.200. It consisted of all the given data as independent variable with hours-per-week as the dependent variable.
We then used a combination of backward p-elimination method and evaluation of adjusted R-squared, AIC and BIC values to arrive at a harmonious reduced model which has an R-squared value of 0.199. We have removed insignificant variables while keeping an Adjusted R-squared value as high as 0.198 and AIC and BIC values lesser than the full model. Refer to the Appendix part 2 for details on the R-squared, AIC and BIC values.
To further improve the model, we explored few interaction term effects on the independent variable. We assessed the interaction between the education and sex, workclass and education. We wanted to see if the sex impacts the effect of education on workhours. We plotted the values to see if there is any interaction and since there was, we included them to the model (Appendix Part 2). It resulted in a slight increase in the R-squared value and further decrease in the AIC and BIC values.

### Question 6
We regressed the work hours with data for people who work in Sales. With just comparing the R-square values, there was more improvement when we ran the model for people who work in Sales. The R-square value went up to almost 0.3. The AIC and BIC values reduced by a large value. One of the reasons could be because the model fit the specific data on Sales people better than all the data points. The degree of freedom is also less for this model which explains the difference in the metrics.
The model showed improvements when we removed least significant variables like native country. It explains that the works hours is not impacted by the native country. 
 
