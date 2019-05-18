# Lecture 14 (Week 7, Wednesday)

## Sampling Distributions (continued)
* a **sampling distribution** is a distribution of sample statistics, or estimates
  * each row in data frame represents an entire sample that you collected
* a **data distribution** is a distribution of individual data points
  * each individual observation represents one case in your data frame
  
### Distribution Triad: What Distribution do Estimates Come From?
* a **sampling distribution** is a model of the distribution of estimates
* distribution of DGP will look similar to that of the sample
* we don't really know what the DGP looks like
* if we make our sample larger, it will more and more resemble our population
  * how do we know this is true?
  * if we made our sample large enough to include the entire population, it would look exactly like the population
* sampling distributions are imaginary
* any parameter estimate can be thought of as coming from a sampling distribution of all possible samples of the *same size* that could have been drawn from the same DGP
* when creating a sampling distributions, the samples must be of the same size

### Why We Need a Sampling Distribution
* to put context around our sample statistics or parameter estimates
* what distribution did b<sub>1</sub> come from? could it have come from a DGP with a β<sub>1</sub> = 0?
  * b<sub>1</sub>: difference in means between two groups, increment from group 1 to group 2
  * comparing two models where we are just using the model as a predictor (b<sub>1</sub> = 0) and a model where we have a b<sub>1</sub>
  * we need the more complex model - as indicated by the difference
* maybe the difference is just due to sampling variation?
* use of a sampling distribution is to help take the difference that we observed and say could that difference just have occurred through random sampling?

### Drawing Distributions
* what is the probability, just by chance, that you would get a b<sub>1</sub> of 1.9?
* can only answer this question using the sampling distribution
* use sampling distribution for finding the likelihood of a sample statistic occurring
* use data distribution for finding the likelihood of an individual data point occurring
* when doing a simulation, you're setting up the 'if' part of the sampling distribution
* β<sub>1</sub> = 0, what is the probability that our sample and b<sub>1</sub> occurred by chance?

## Simulating a Sampling Distribution of b<sub>1</sub>
If β<sub>0</sub> = 100 (mean), σ = 15, and β<sub>1</sub> = 0, what is the probability of randomly choosing 2 groups of n = 5 each and getting a difference of greater than 5?
* draw a picture to represent this question

Casting the Question as Model Comparison
* what are the chances that our sample estimate b<sub>1</sub> could have come from a DGP with β<sub>1</sub> = 0?
* to answer this question we need to simulate this sampling distribution

What does this code do?
````
outcome <- rnorm(n=10, mean=100, sd=15)
````
* generates 10 data points from a distribution with a mean of 100 and sd of 15
* you get a new graph every time you run this code
* the mean is different each time; difference is caused by *randomness*
* to simulate b<sub>1</sub>, you need a second grouping variable
````
group <- rep(letters[1:2], each = 5)
````
* two groups randomly selected from a population and find the difference in means between those two populations
* put them into a data fram
````
study <- data.frame(group,outcome)
````
* make histograms and mark the means
* both groups seem to be hovering around outcome of 100
* more likely than not, the scores we sample will be around 100
* is this a sampling distribution?
  * no, this is a single sample
  * for a sampling distribution, need to do this 100+ times
````
b1(outcome~group, data=study)
````
* calculates b<sub>1</sub>
* varies by a lot each time you run this code
* to make a sampling distribution, surround it with the do command
````
SDoB1 <- do(1000)* {
  outcome <- rnorm(n=10, mean=100, sd=15)
  group <- rep(letters[1:2], each = 5)
  study <- data.frame(group,outcome)
  b1(outcome~group, data=study)
}
````
* makes it run 1,000 times
````
head(SDoB1)
````
* each number is a b<sub>1</sub>
* 1,000 rows with 1 variable
* make a histogram to produce a sampling distribution

Sampling distribution of b<sub>1</sub>: What is "count" the count of?
* why do you think this distribution is centered at 0?
  * because the samples are drawing from the same DGP, which is centered at 0

### Thinking in "What If" Statements
What is the probability that you will get a b<sub>1</sub> > 5?
````
tally (~result > 5), data=SDoB1, format="proportion")
````

### Some More "What Ifs"
How would probability be affected by:
* increasing sample size
  * replace 10 with 100
  * histogram (use scale refine)
  * sampling distribution is much narrower with a larger sample
  * probability of getting > 5 will now be lower
  * there are fewer samples
  * confirm with `tally`
* increasing DGP mean from 100 to 120
* changing DGP SD to 10 from 15
