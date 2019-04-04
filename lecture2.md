# Lecture 2 (Week 1, Wednesday)

>“Robert Martin was laid off from his job at Westvaco, Inc. soon after he turned 54 years old. He sued for age discrimination.”

What kind of data would we need to evaluate this claim?

| ages of employees in one department (~~laid off~~) |
|:--------------------------------------------------:|
| 25, 33, 35, 38, 48, ~~55~~, ~~55~~, 55, 56, ~~64~~ |

What makes a data structure tidy?
* structure 1 is not tidy because each row is not an observation

## Make a data frame
* name it Westvaco
* start with two vectors, use data.frame( )
* print out the data frame

````
age <- c(25,33,35,38,48,55,55,55,56,64)
fired <- c("no", "no", "no", "no", "no", "no", "yes", "yes", "no", "yes")
westvaco <- data.frame(age,fired)
westvaco
````

## Visualize the distribution
* make a histogram of age
* make a faceted histogram of age by fired
* make a boxplot of age by fired

````
gf_histogram(~ age, data=westvaco, fill="blue", binwidth=1)%>%
gf_facet_grid(fired ~.)
````

Based on these data, do you think Westvaco's pattern of firings shows evidence of age discrimination?

## Modeling Data & DGP
* fired = age + other stuff
* what are some other possible models
* **data = model+ + error**

Based on the data, do you think the pattern of firings could be explained by a purely random DGP?

**Key point:** you can't see evidence of randomness by just looking at a single outcome.
(You have to flip a coin more than once to tell if it is fair.)

## Simulating Randomness
Adding in Sampling Distributions
