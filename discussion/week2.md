# Week 2 Discussion

## Purpose of statistical models
1. help understand DGP
2. let us make predictions about future observations

* data = model + error
* if we have no explanatory variable, what statistical model do we typically use to describe data?
  * mean

## Mean as a statistical model
* why do we use the mean?
  * produces model with lowest error
  * data = model + error → data = mean + error
* why is an empty model "empty?"
  * Data = Mean + other stuff (yes)
  * Data = Median + other stuff (yes)
  * Data = Explanatory Variable + other stuff (no)
  * Height = Mean + other stuff (yes)
  * Height = Sex + other stuff (no)
  * FiveVegetable = Pres2008 + other stuff (no)
  * FiveVegetable = Median + other stuff (yes)
* what makes an empty model empty?
  * no explanatory variable
  
## Revisiting Notation: Parameter vs. Statistic
* write a word equation for each mathematical equation - the outcome variable is height
  * Height = Mean (y-bar) + other stuff
  * Height = Model (y-hat) + other stuff
* reviewing model notation
  * Y<sub>i</sub>: one individual's score
  * Y-bar: mean of all scores
  * B<sub>0</sub>: data mean
  * β<sub>0</sub>: population mean (can't be measured, only estimated)
  * e<sub>i</sub>: one individual's error from the data mean
  * ε<sub>i</sub>: one individual's error from the population mean
* statistics (sample): Y-bar, b<sub>0</sub>, e<sub>i</sub>
* parameters (population: β<sub>0</sub>, ε<sub>i</sub>
* what is the difference between b<sub>0</sub> and Y-bar?
  * Y-bar always represents the mean
  * b<sub>0</sub> could represent the mean, but it could also represent the median
* what is the difference between b<sub>0</sub> and β<sub>0</sub>?
  * β<sub>0</sub> represents the population
  * b<sub>0</sub> represents the sample statistic
  
## Quantifying Error: Sum of Squares
* calculate the **residual** of **Height** in the **Fingers** dataset
````
Empty.model <- lm(Height ~ NULL, data = Fingers)
Empty.model
````
* save the residuals as a new varaible **Height.residual** to the **Fingers** dataset
````
Fingers$Height.residuals <- resid(Empty.model)
str(Fingers)
````
````
Fingers$Height.residuals.2 <- Fingers$Height - 65.95
str(Fingers)
````
* use the `sum()` function to calculate the total Height error (aka residuals)
````
sum(Fingers$Height.residuals)
````
* what do you get as a result?
  * `-1.953993e-14`
  * shows us that there is basically no variation in our data
  * not a very good way to quantify error
````
Fingers$sq.residuals <- Fingers$Height.residuals ^ 2
str(Fingers)
sum(Fingers$sq.residuals)
````
