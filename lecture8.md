# Lecture 8 (Week 4, Wednesday)

## Error (continued)
* how much does Penelope the cow weigh?
* distribution of 17, 205 guesses: what is the shape of this distribution? skewed
* why do you think the mean guess is so close to Penelope's actual weight?
  * partitioning individual scores into model + error
  * error will all cancel out
  * mean is a powerful predictor
  
## Quantifying Error: Sum of Squares
* null model tells us how much total variation we have

````
MiamiHeat$Assists.group <- ntile (MiamiHeat$Assists, 2)
favstats(Points~Assists.group, data = MiamiHeat)
````
````
favstats(Assists ~ Assists.group, data=MiamiHeat)
````
````
gf_histogram(~Points, data=MiamiHeat, fill="orange") %>%
gf_facet_grid(Assists.group ~ .)
````

* points = mean + error vs. points = assists + error
  * which model has more error? the empty model
  * same variation in data, but once the model is applied, it is just the error around the prediction
  * most error you will have is in the null model - no explanatory variable
  
Least squares estimation of best fitting model:
* using estimators (such as the mean) at which the sum of squares is minimized
* null model: SS = Σ (Y<sub>i</sub> - Y-bar)<sup>2</sup>
* any model: SS = Σ (Y<sub>i</sub> - Y-hat)<sup>2</sup>

## Variance and Standard Deviation
Limitations of SS
* where is Points more variable? in Wins or in Losses?
````
Empty.win <- lm(Points ~ NULL, data = filter(MiamiHeat, Win == "N"))
anova(Empty.win)
````
````
Empty.lose <- lm(Points ~ NULL, data = filter(MiamiHeat, Win == "L"))
anova(Empty.lose)
````
* sum of squares
  * wins: 5689, losses: 1748
* why is the SS for points so much larger for wins than for losses?
* variance is a measure that corrects for sample size
* average amount of variance per degree of freedom
* **variance** is sum of squares per unit (or per df) in the sample
* sum of squares can be partitioned into Total, Model, and Error
* variance and standard deviation don't add up the same way
* where can you see "see" the 2.9 in the histogram?
  * estimate the standard deviation of Assists
  * roughly 2/3 is within 1 SD of the mean
* describe Game 20 using SD as a measure
  * half of a standard deviation below the mean
* where in the picture is z? s? (Y<sub>i</sub> - Y-bar)?

What's the point of Z? (power of division)
* to put things on a scale where we can compare them across different distributions with different measures

Why model error?
* use the model to make a prediction?
* what are the chances that the Miami heat will make more than 15 3-points in the next game?
  * to answer this question, need to use data distribution as probability distribution
  * normal distribution: in both models, total area adds up to 100%
