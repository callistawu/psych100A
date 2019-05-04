# Lecture 10 (Week 5, Wednesday)

## Adding an Explanatory Variable to the Model
* which diagram shows error from the empty model; which the two-group model?
* explanatory models seek to reduce error
  * partition variation into explained and unexplained (error)
* what is sum of squares?
  * statistic, not a parameter
  * anything you can calculate based on your data is a statistic
  * parameter is unknown because we don't know about the population

## Vegemite.brief (continued)
* spoon2. difference by Respect
  * respect, or random?
  * does Respect explain some of the variation? the means are different
  * what are the possible causes of this mean difference?

## Shuffle Exercise: Exploring the Random DGP
* shuffle the Respect variable
* make a new variable based on the variable respect.condition
````
Vegemite.brief$respect.shuffle <- shuffle(Vegemite.brief$respect)
str(Vegemite.brief)
````
````
tally(~respect.condition, data=Vegemite.brief)
````
````
tally(~respect.shuffle, data=Vegemite.brief)
````
  * outputs are the same because we've just shuffled the people within the two categories
````
head(select(Vegemite.brief, respect.condition, respect.shuffle, spoon2.difference))
````
````
Vegemite.brief$respect.shuffle <- shuffle(Vegemite.brief$respect)
gf_histogram(~spoon2.difference, data=Vegemite.brief, fill="orange") %>%
gf_facet_grid(respect.shuffle~.) %>%
gf_vline(xintercept=~mean, data=favstats(spoon2.difference~respect.shuffle, data=Vegemite.brief))
````
  * the mean difference changes every time you run it
  * completely random pairings of conditions, so the results are varying randomly
  * gives us the context for judging how likely the results we got are random

* what are the possible causes of the mean difference in this shuffled distribution?
  * these are not the results of our study
  * the only possible cause is **randomness**
  * we simulated the data generating process; we know it's random
  * eventually, if we run this enough times, we will produce results that look like the actual results we got
* the mean of spoon2.difference does not change
* the fact that we have to run this so many times suggests that our results are not only due to random chance

## DATA = MODEL + ERROR
* vegemite eaten = respect + error
  * GLM notation: Y<sub>i</sub> = b<sub>0</sub> + b<sub>1</sub>X<sub>i</sub> + e<sub>i</sub>
  * b<sub>0</sub> = mean of group 1
  * b<sub>1</sub> = increment you need to add to group 1 to get the mean of group 2
* vegemite eaten = mean + error
  * GLM notation: Y<sub>i</sub> = b<sub>0</sub> + e<sub>i</sub>
  * null model

### Using Vegemite.brief data, fit and save two models of spoon2.difference: empty.model & respect.model.
````
empty.model <- lm(spoon2.difference ~ NULL, data=Vegemite.brief)
respect.model <- lm(spoon2.difference ~ respect.condition, data=Vegemite.brief)
empty.model
respect.model
````

### Using the Model to Make Predictions
* Y<sub>i</sub> = 0.138 + 0.088 * Respect<sub>i</sub> + e<sub>i</sub>
* Y-hat<sub>i</sub> = 0.138 + 0.088 * Respect<sub>i</sub>
  * no error term because this is just a prediction
  * we don't know the error to predict

As the researcher, which parameter are we most interested in?
* β<sub>0</sub> in the empty model,  β<sub>0</sub> in the two-group model, or β<sub>1</sub> in the two-group model?
  * both β<sub>0</sub> and β<sub>1</sub> in the two-group model

### Save the predicted & residual scores from the two models into the Vegemite.brief data frame.
Predicted and Residuals from the Empty Model
````
Vegemite.brief$empty.predict <- predict(empty.model)
Vegemite.brief$empty.resid <- resid(empty.model)
head(select(Vegemite.brief, respect.condition, spoon2.difference, empty.predict, empty.resid))
````
Predicted and Residuals from the Two-Group (Respect) Model
````
Vegemite.brief$respect.predict <- predict(respect.model)
Vegemite.brief$respect.resid <- resid(respect.model)
head(select(Vegemite.brief, respect.condition, spoon2.difference, respect.predict, respect.resid))
````
  * the comparison between the two models will tell us how much error was reduced
