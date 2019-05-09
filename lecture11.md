# Lecture 11 (Week 6, Monday)

## Vegemite
* why do some people eat more vegemite than others?
* explore variation: make a scatterplot to see whether respect_condition explains variation in veg_eaten
  * veg_eaten = respect + error

````
library(readr)
vegemite_clean <- read_csv("http://bit.ly/vegemite_clean")
gf_point(veg_eaten ~ respect_condition, data = vegemite_clean)
gf_jitter(veg_eaten ~ respect_condition, data = vegemite_clean, width=.1, height=0, size=5, alpha=.3, color="darkolivegreen4")
````
## Model Variation
### 2) Draw the models onto the jitter plot.
* draw in the empty model
  * straight line at 0.1836
  * predicts the same for everybody
* draw respect model
  * thinks there are two different groups
  * predicts something different for different people
  * for the no respect group, predict 0.14
  * for the respect group, predict 0.14 + 0.09
* why jitter plots come in handy:
  * veg_eaten = respect + model
* let's draw the models onto the jitter plots in R

````
empty.model <- lm(veg_eaten ~ NULL, data = vegemite_clean)
respect.model <- lm(veg_eaten ~ respect_condition, data = vegemite_clean)
````
````
vegemite_clean$empty.pred <- predict(empty.model)
vegemite_clean$empty.pred <- predict(respect.model)
````
````
gf_jitter(veg_eaten ~ respect_condition, data = vegemite_clean, width=.1, height=0, size=5, alpha=.3, color="darkolivegreen4") %>%
gf_jitter(empty.pred ~ respect_condition, color="blue", height=0) %>%
gf_jitter(respect.pred ~ respect_condition, color="orange", height=0)
````
### 3) Just by looking, is there left over variation from the respect model?
* we've predicted very little

### 4) What would the data look like if the respect model explained 100% of variation?
* that's never how data looks

## Draw the Residuals
### 5) empty model's residuals vs. respect model's residuals
* residuals balance each other out

### 7) Isn't the error from the empty model always bigger than error from the complex model?
* yes, always
* true at the aggregate level
* not true at the level of individual data points

Error at Two Levels
* individual data points: residuals
* aggregated (the whole distribution): SS
  * always bigger for the empty model

### 8) Draw a few squared residuals that go with each SS.
* green boxes + orange boxes = blue boxes

Run supernova( ) on both the **empty.model** and the **respect.model.**
````
supernova(empty.model)
````
  * sum of squares: empty model
````
supernova(respect.model)
````
  * no matter what the complex model is, SS total stays the same
  * is 0.311 a lot of error reduced? difficult for us to tell

PRE: Converting Squared Error Units into Proportion
* how would you calculate PRE from these three sums of squares?
* (SS Total - SS Error) / SS Total
