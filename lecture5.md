# Lecture 5 (Week 3, Monday)

## Explaining Variation: Working Definition
Knowing someone's value on the explanatory variable helps you make a better guess about their value on the outcome variable.

Knowing someone's value on sex helps you make a better guess about their height.
* height = sex + other stuff
* variation in data = explained + unexplained

Does sex explain age?
* Age ~ Sex
* no, the distributions look like they're lined up on top of each other

Does marital status explain age?
* Age ~ Married
* yes, to some degree, because the medians are different

Does marital status explain *more* of age than sex?

**Tetris Data:** Does Condition explain number of Intrustions_1_7?
* graph 2 is different from the others

## Sources of Variation
* variation in data: explained (measured) + unexplained (measured)
* explained: causal + non-causal
* unexplained: real (characteristic of system) + induced (by data collection)

## New Data Frame: USStates
* look at the contents
* create a histogram of FiveVegetables

````
str(USStates)
gf_histogram(~FiveVegetables, data=USStates, fill="skyblue", color = "purple", bins=8)

````
* what do the numbers on the y-axis mean?
  * number of states

Visualize the relationship between Pres2008 and FiveVegetables.
* FiveVegetables = Pres2008 + Other Stuff

````
str(USStates)
gf_histogram(~FiveVegetables, data=USStates, fill="skyblue", color = "purple", bins=8) %>%
gf_facet_grid(Pres2008 ~ .)
````
* does Pres2008 explain variation in FiveVegetables in our data?
  * yes, somehow you can make a better guess
  * Obama states tend to eat more vegetables
* does Pres2008 explain variation in FiveVegetables in the DGP?
  * not sure yet

Two Quantitative Variables
* does Smokers explain variation in FiveVegetables in our data?
  * yes, you can draw a line at the mean of Smokers and a line in the middle of FiveVegetables
  * helps to predict
* do people who smoke eat fewer vegetables?
  * no / not sure, it's not supported by the data
  * the data is based on the *state*; it doesn't tell you anything about individual people
  
## Statistical Models
* FiveVegetables = Other Stuff
* FiveVegetables = Pres2008 + Other Stuff
* Variation is explained. But how much is explained? Statistical models help us quantify how much.

### What is a Model?
* what is error?
  * the part where we're wrong
* what is "best fit"?
  * somewhere in between; tries to minimize errors to the extent possible
* what is a **statistical model**?
  * a mathematical function used to generate predictions
  * how does this improve on our previous definition of *explain?*
* what should you predict for this state?
  * all we know is who they voted for president

### Comparing models
* FiveVegetables = mean + other stuff
* FiveVegetables = Pres2008 + other stuff
* if you use mean as prediction, which model has more error?

## The Empty Model
* the simplest statistical model uses a single number to represent a distribution - for example, the mean
* error is the part that doesn't fit within the model
* if you had to pick just one number to represent a distribution... it can be, but doesn't have to be, the mean
* `okcupid` data: what number? why useful? what counts as error
  * can't take the mean of categorical variables
  * pick the mode or median

### DATA = MODEL + ERROR (literally)
* every data point can be partitioned into model + error
* residual
* the empty model tells us how much total error there is in the outcome - error we try to reduce by adding explanatory variables
