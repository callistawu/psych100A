# Lecture 7 (Week 4, Monday)

## Review: Empty Model
* empty model gives us a hint to how much variation we need to explain
* every data point can be partitioned into model + error
* error doesn't really exist unless you have a model
* last week: 
  * `lm()`, `predict()`, `resid()`
  * using the mean as the model
* **notation:** what GLM notation would you use to represent the numbers inside the rectangle? Y<sub>i</sub>

## This Week: Focus on Error
* aggregating error to assess model fit
  * once you have the data, asking the question: how well does the model fit the data?
  * quantifying how much error is around the model
  * how much error is reduced when using a more complicated model
* modeling the distribution of errors to make prediction

## Dataframe MiamiHeat
* is the study a correlational design or experimental design?
  * correlational because we're not manipulating any variables
  * data that naturally arose in a season of basketball
* what are the rows in the data frame?
  * games
* let's use Points as the outcome variable
  * where's the variation in points? (horizontal)
  * where's the variation in games? (vertical)
  * word equation: Points = FG + other stuff
  * explore the relationship graphically: does your explanatory variable appear to explain variation in points?
    * scatterplot, faceted histogram, boxplot
  * what would the empty/null model be that we would compare to our complex model?
    * write as a word equation: Points = Mean + other stuff
    * write in GLM notation: Y<sub>i</sub> = b<sub>0</sub> + e<sub>i</sub>
  * fit the empty model (save the empty model in an object called Empty.model) `lm()`
 ````
 Empty.model <- lm(Points ~ NULL, data = MiamiHeat)
 ````
 * example: 
  * assists model: points = assists + error
  * empty/null model: points = mean + error
  * what is the mean here the mean of? the mean is the mean of points (mean of outcome variable)
  * which model would have the most error? the empty model (that's all the error in the outcome variable)
  * model + error = 100% of variation in outcome
    * assists model explains ?% of error
    * empty model explains 0% of error
  * use data to create model of DGP

## Explaining Variation
* histogram: where is the model? where is the error?
* where would you draw the empty model on the scatterplot?
  * horizontal line at the mean of Points

## Aggregating Error to Indicate Model Fit
* empty model is a single number, but not just any number - a number that will give us the lowest amount of error possible

### Why the Mean
* mean as an estimator is: unbiased, efficient, consistent
* and: lots of techniques have been worked out using the mean as an estimator (i.e. `lm()`)
* but:
  * assumes that errors are distributed normally
  * and we have new techniques for computational modeling that make it easier to use other estimators (e.g. the median)
* what indicator of total is minimized at the mean?

### We Cannot Use Sum of Residuals
* fit the empty model to Points and save in Empty.model
* save the residuals from the empty model into a new variable: MiamiHeat$Resid.points
````
MiamiHeat$Points.resid <- resid(Empty.model)
head(select(MiamiHeat, Points, Points.resid))
````
* sum the residuals
````
sum(MiamiHeat$Points.resid)
````
  * we can't use this as an indicator of an aggregation of error because it is too close to zero
* sum of squares
* how many methods can you find to use R to calculate the sum of squared errors?
  * `sum(MiamiHeat$Points.resid^2)`
  * `sum((resid(Empty.model)^2))`
  * `anova(Empty.model)`
* confirm: is SSE really the smallest at the mean?
  * SSE at mean was 10,485
  * calculate SSE for other possible models
  * start with 102.06
  * `sum((MiamiHeat$Points-102.06)^2)` gives the SSE 102.06
  * `sum((MiamiHeat$Points-103)^2)` gives the SSE 10557
  * `sum((MiamiHeat$Points-104)^2)` gives the SSE 10793

##$ Sum of Absolute Errors
````
sum(abs(MiamiHeat$Points-mean(MiamiHeat$Points)))
sum(abs(MiamiHeat$Points-median(MiamiHeat$Points)))
````
* SSE is minimized at the mean
* no other number will produce a lower Sum of Squares than the mean of the distribution
* SAE is minimized at the median
