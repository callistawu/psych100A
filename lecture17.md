# Lecture 19 (Week 9, Wednesday)

## Sampling Distributions to Confidence Intervals (continued)
Comparing simulated and randomized sampling distributions of b<sub>1</sub>
* why do you think the simulated sampling distribution looks more normal?
* simulated sampling distribution came from a normal distribution
* we don't know the shape of the actual data

## Confidence Intervals
* we can construct a new copy of the sampling distribution, centered at our sample mean

### Using the Randomized Sampling Distribution
* how can we calculate the confidence interval from this distribution?
  * move this distribution so that it's centered at 1.9
  * then find the lowest and highest 2.5%
  * or, calculate the standard error based on this distribution

Finding the 95% Cut-off Points
* how do we get from this to a confidence interval?
````
confint(lm(Games~Condition, data = ScienceData))
````
