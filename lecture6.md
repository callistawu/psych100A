# Lecture 6 (Week 3, Wednesday)

## The Sample and the DGP
* data generative process
* sampling variation - the sample is not representive of the DGP
* process that produces variation in the real world and variation in our data

## Statistical Model
* a mathematical function used to generate a prediction
* how does this improve upon our previous definition of *explain?*
* y = f(x)

## Compairing models
* FiveVegetables = **mean** other stuff
* Why do we need the empty mode?
  * add explanatory variables to explain error
`FiveVegetables = *mean* _ other stuff`
if you use mean as prediction, which has less ordrer

##Notation
* use different  notations to differentiate (view diagram)

##Parameters and Statistics
Key points about models
* statistical models constructed from data, but used to model the DGP
* models serve two key functions:
  * help us understand DGP
  * help us understand distribution

## Fitting the Empty Model
* what does it mean to "fit" a model?
* use lm( ) to fit the empty model for FiveVegetables
````
lm(FiveVegetables ~ NULL, data = USStates)
````
* what is the 23.44? (intercept)
  * parameter estimate for the empty model
  * mean of FiveVegetables
  * the MODEL part of MODEL + ERROR
* what is the 23.44 in GLM notation? b<sub>0</sub>

### Generating Model Predictions
* can you think of another way to fit the empty model?
* use the `predict( )` function to generate model predictions for the empty model of FiveVegetables
* solve the predictions in a new variable in the USStates data frame called empty.predict
* look at the data frame to see if your new variable is there
````
empty.predict <- predict(lm(FiveVegetables ~ NULL, data = USStates))
empty.predict
````
````
USStates$empty.predict <- predict(lm(FiveVegetables ~ NULL, data = USStates))
str(USStates)
````
````
predict(lm(FiveVegetables ~ NULL, data = USStates))
````
````
head(select(USStates, State, FiveVegetables, empty.predict))
````
* why does every state have the same value for empty.predict?
  * this is the empty model - each state will have the same predicted value

### Generating Residuals
* use the `resid( )` function to get the residual for each state from the empty model for FiveVegetables
* save it in a new variable called empty.resid
````
USStates$empty.resid <- resid(lm(FiveVegetables ~ NULL, data = USStates))
str(USStates)
head(select(USStates, FiveVegetables, empty.predict, empty.resid))
````
* why are some of the values negative and some positive in the empty.resid column?
* what GLM notation would you use to represent each of these residuals? e<sub>i</sub>
* where in this printout is DATA, MODEL, and ERROR?
  * DATA = FiveVegetables
  * MODEL = empty.predict
  * ERROR = empty.resid'

### Graphing Residuals
* imagine you make two histograms: one of FiveVegetables, and the other of empty.resid - how will they compare?
  * same shape, but different center
  * same histogram, subtracted from the mean
````
gf_histogram(~FiveVegetables, data=USStates) %>%
gf_histogram(~empty.resid, data=USStates)
````
* adjust scale
````
gf_histogram(~empty.resid, fill="orange", data=USStates) %>%
gf_refine(scale_x_continuous(limits=c(-10,10)))
````

### Summing Residuals
* use R to sum the residuals for the 50 states from the empty model (empty.resid)
* think of the two different method for doing this
````
sum(USStates$empty.resid)
sum(resid(lm(FiveVegetables ~ NULL, data = USStates)))
````

### DATA = MODEL + ERROR
