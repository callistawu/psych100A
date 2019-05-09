# Week 5 Discussion

## DATA = MODEL + ERROR
* StudentSurvey Data
* sum of error<sup>2</sup> = 1.276
* total SS (error) = 1.28
````
empty <- lm(GPA ~ NULL, data = StudentSurvey_small)
supernova(empty)
````
* SS / df = MS
* mean SS error (variance)


## Quantifying Error (e.g. SSE, MSE)

Does Gender explain variation in GPA? (10 observations)
````
empty <- lm(GPA ~ Gender, data = StudentSurvey_small)
````
* coefficients:
  * intercept: 2.945
  * GenderM: 0.075
* what is the model prediction for females?
* what is the model prediction for males?
* how are males and females coded in the data?

GLM Notation
* Y<sub>i</sub> = (b<sub>0</sub> + b<sub>1</sub>) + e<sub>i</sub>
* (b<sub>0</sub> + b<sub>1</sub>) = Y-hat
* what are the values for b0 and b1? where can we find them?


## Two Group Models

GPA By Sex
* how did we calculate the model predictions?
* how are these model predictions different from the empty model predictions?
* does Gender explain variation in GPA?
* does Gender explain variation in GPA?


## Measures of Effect Size (e.g. PRE)
* proportion reduction in error
* what proportion of the total error is explained by our model?
* PRE = SS Model / SS Total

Does Award explain variation in GPA?
````
empty <- lm(GPA ~ Award, data = StudentSurvey)
````
* Y<sub>i</sub> = (b<sub>0</sub> + b<sub>1</sub>)X<sub>i</sub> + b<sub>2</sub>Z<sub>i</sub>+ e<sub>i</sub>

## Comparing Models (F ratio)
* looking at both Gender and Award models
* which model explains a greater proportion of the variance in GPA?
* which model is more "complex"? what statistic tells us this?
* which statistic gives a sense if the **variation explained** by the model is worth its **complexity?**
