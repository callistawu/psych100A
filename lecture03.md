# Lecture 3 (Week 2, Monday)

## Recap: Robert Martin Example
* distribution is the lens through which we view variation
* do you think the data supports the claim of age discrimination?
* we can't really evaluate Robert Martin's claim, so we should create a distribution

| ages of employees in one department (~~laid off~~) |
|:--------------------------------------------------:|
| 25, 33, 35, 38, 48, ~~55~~, ~~55~~, 55, 56, ~~64~~ |

* made a histogram and faceted histogram
* `%>%` layers a command onto a previous command

## Informal models: Word equations
* data = model + error
  * fired = age + other stuff
  * fired = experience + other stuff
  * fired = other stuff

## Model Comparison: Can We Rule Out the Purely Random Model?
* fired = age + other stuff
* fired = other stuff
  * empty model (null)
* if we can simply rule out the simpler model, we will need to go with the more complex one
* you can't judge randomness by just looking at a single outcome (in poker, "resulting")

We know how to model purely random processes. Using tools of statistics:
* we ask: **if** purely random model is true, what is the likelihood of getting a data distribution -- ?

## Simulating Randomness: Adding in Sampling Distributions
  1. Simulate process
  2. Construct summary of outcome
  3. Repeat

**How to simulate random DGP for Westvaco?**

  1. Construct materials: 10 pieces of paper, each with one of the ages
  2. Simulate random selection of 3 to fire
  3. Enter your three selected ages: [bit.ly/randomages](https://bit.ly/randomages)
  
````
westvaco.sim <- read.csv("http://bit.ly/westvacosimulation", header = TRUE)
head(westvaco.sim)
````

* create average age fired as a new variable in data frame

````
westvaco.sim$meanAge <- (westvaco.sim$Fired1 + westvaco.sim$Fired2 + westvaco.sim$Fired3)/3
head(westvaco.sim)
````

* now use R to examine the distribution of random draws
  
````
favstats(~meanAge, data = westvaco.sim)
````

````
favstats(westvaco.sim$meanAge)
````
* make a histogram

````
gf_histogram(~meanAge, data=westvaco.sim, fill="dodgerblue")
````

* what does the count on the x-axis refer to on this distribution?
  * number of random samples drawn from a hat
* **sampling vs. data distribution**
  * where are fired employees represented in each graph?
  * data: y-axis is number of people that age in the sample
  * sampling: y-axis is the number of random samples that were drawn

Back to our Model Comparison Question
* fired = age + other stuff vs. fired = other stuff (empty model/null hypothesis)
* if the DGP is random --
  * `meanAge >= 58`
  * what is the probability of getting a sample with `meanAge >= 58`?

````
tally(~meanAge >= 58, data=westvaco.sim)
````

You are the lawyer for Robert Martin. How can you use this sampling distribution to support your claim of discrimination?

You are the lawyer for Westvaco. How can you use this sampling distribution to support your claim against discrimination?
