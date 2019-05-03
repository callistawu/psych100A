# Lecture 9 (Week 5, Monday)

## Review
* **error** = the difference between what your model predicts and what your actual scores are in the data
* **randomness** = data generating process; the process that generates variation
* variation in data, when put in a model, becomes error

## Overview of Explanatory Models
### Empty Model Gives Birth to Error
* SS tells us how much total error
* where exactly, does the empty model minimize error?
  * in the sample distribution
  * we don't know the error in the population distribution
  * error = residual = score - predicted
  
### Explanatory Models Seek to Reduce Error
* trying to reduce error in the outcome variable
* if we add an explanatory variable, can we reduce error?
* how should we interpret sum of squares from the empty model?
  * amount of unexplained variation in the outcome variable
  * in empty model, all the variation is unexplained

### SS From Empty Model Quantifies Total Error
* **SS Total** = total variation in outcome, adds up to 100%
* by reducing model down, some of our variation has been explained

## Two-Group Model - Specifying
* total error is unchanged
* reducing unexplained error increases explained error
* data = group + error
* how much is error reduced in the GROUP model vs. the EMPTY model?
* empty model lets us partition each score into model (mean) + prediction
* explanatory models let us reduce error
* now we can partition each score into error from the model, and error reduced from the empty model

## Fitting, Predict, Resid (Partitioning Scores)
### Can Respect Improve Medical Adherence?
* **hypothesis:** respectful instructions will create better medical adherence (especially in adolescents)
* study procedure
  * taste instruction (spoon 1)
  * watch video instructions (respectful or not)
  * how much medicine did they eat? (spoon 2)
* look at data fram `Vegemite.brief`
````
Vegemite.brief <- select(Yeager.Vegemite.Data, r.condition, spoon2.difference)
head(Vegemite.brief)
````
* each row is a participant
* what would a value of 0 on the outcome variable mean?
  * they didn't eat any of the vegemite
  * difference between what they were given and what they ate was 0
  
### Explore the Distribution of the Outcome Variable
````
gf_histogram(~spoon2.difference, data=Vegemite.brief, fill="green") %>%
gf_facet_grid(respect.condition~.) %>%
gf_vline(xintercept=~mean, data~favstats(spoon2.difference~respect.condition, data=Vegemite.brief))
````
* bimodal distribution, people either ate all of it or nearly none of it
* what are the possible causes of the mean difference?
  * randomness
  * consequences of respect conditions
