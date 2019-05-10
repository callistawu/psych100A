# Lecture 12 (Week 6, Wednesday)


##### Fitting the Empty Model and the Two-Group Model
* two-group model: replace null with explanatory variable in R
* vegemite_eaten = respect.condition + error
* GLM notation

As a researcher, which parameter are the researchers most interested in?
* β<sub>1</sub> in the two-group model
* care about the difference

## Error in the Two Models
* error at two levels at two levels: as residuals, and as totaled up in sum of squares
* blue line = grand mean
* black line = two-group model, makes 2 different predictions
* each residual can be divided up between the part from the empty model and the part from the two-group model
* SS Total is based on deviation
  * (score - model prediction)<sup>2</sup>
* for a data point right here, which model produces a better predicted score?
  * empty model
  * because the data point is closer to the empty model than the predicted model
  * on average, not closer to the empty model though
````
lm(spoon2.difference ~ respect.condition, data=Vegemite.brief)
````
* can you tell from the model fit how much of the variation in outcome is explained?
  * no
  * there's nothing in the model fit that tells you percent of variation
  * model fit basically gives you two group means, but nothing about variation
  * need to look at `supernova()` or `anova()` table

Run `supernova()` on both the **empty.model** and the **respect.model.**
* sum of squares: empty model
  * `supernova(empty.model)`
* sum of squares: two-group model
  * `supernova(respect.model)`
* total sum of squares is the same for both of these models
* which part represents the unexplained error from the empty model?
  * SS Total
  * SS Error is what is leftover when we apply the two-group model

## Three-Group Model
### New Model for spoon2.difference: Test3Group
* how would you write the model specification for the Test3Group model?
  * Y<sub>i</sub> = b<sub>0</sub> + b<sub>1</sub>X<sub>i</sub> + b<sub>2</sub>X<sub>2</sub> + e<sub>i</sub>
  * 3 parameters, one for each group

````
Test3Group.model <- lm(spoon2.difference ~ Test3Group, data=Vegemite.brief)
Test3Group.model
supernova(Test3Group,model)
````

Why are SS Total the same for Respect and Test3Group?
* trying to explain the same outcome variable

Why is PRE different?
* SS Model / SS Total
* respect condition accounts for more variation than does Test3Group

Why are df same for Total but different for Model?
* for total, we're using the same sample
* for model, it's the number of parameters estimated minus 1

### Comparing Models
Could Model One and Model Two have different outcome variables?
* no because they have the same SS Total

Could Model One and Model Two have different explanatory variables?
* yes, they can explain the same outcome and have the same SS Total

Could Model One and Model Two be based on different samples?
* no; different samples would assumed to have different sum of squares

### Comparing Models with Different Outcome Variables or Samples
How can you compare these two models?

> Everything you know about group models will transfer directly to regression models, with few exceptions.

## Categorical vs. Quantitative Explanatory Variable
### Smoking and Obesity: Comparing Two-Group and Regression Models
* quantitative as the predictor
* exact same data points showed in a different way

How would you divide the points in this scatter plot into the two smoker2group groups?
* they are the dots on either side of the vertical line at the median of Smokers

Model Predictions: Means vs. Line
* model for two-group model is represented by two group means
* model for regression model is represented by regression line
* statistical model is a function
  * mean of group (two-group)
  * slope of the line (regression)
* prediction for two-group model: mean
* prediction for regression model: point on the regression line

Model Specification for Two-Group Model and Regressioon Model
* two-group model: Y<sub>i</sub> = b<sub>0</sub> + b<sub>1</sub>X<sub>i</sub> + e<sub>i</sub>
* regression model: Y<sub>i</sub> = b<sub>0</sub> + b<sub>1</sub>X<sub>i</sub> + e<sub>i</sub>
* how can you tell the difference?
  * look identical
  * you must interpret each component *in context*
  * two-group model: b<sub>0</sub> is mean of first group, b<sub>1</sub> is increment from mean of first group
  * regression model: b<sub>0</sub> is y-intercept, b<sub>1</sub> is slope of the line (how much you add as an increment as a function of one unit increase to predictor variable)
  * function is represented the same way but different meanings
  
Fitting the Two0Group Model and the Regression Model: Same R Code
````
lm(Obese ~ smokers2group, data=USStates)
````
* R treats one as categorical and the other as quantitative

How is Y-hat different from Y<sub>i</sub>?
* Y<sub>i</sub> is your  person i's actual store
* Y-hat is predicted score under predicted model

How is Y-hat different from Y-bar?
* Y-bar is the grand mean
* in a two-group model, grand mean is different from predicted model

### Quantifying Error for Group Model and Regression Model
* same formula for group model and regression model, just a different y-hat
* SS = Σ(Y<sub>i</sub> - Y-hat)<sup>2</sub>
* which sum of squares is this? total, model, or error?
  * SS Error
  * sum of squared deviations from model prediction (mean of group)
