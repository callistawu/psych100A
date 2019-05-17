# Lecture 13 (Week 7, Monday)

## Sampling Distributions
* doesn't really exist, something we have to invent
* we learn a lot about data from their context

### Be Science vs. Do Science
* what is the cause of the mean difference between the Be Scientist group and the Do Science group?
  * both the experimental manipulation and randomness
  * based on size of PRE and F, there is an effect
  * also, if we had taken a different sample, there would have been a different result
  * sampling variation is *always* an issue
* Rhodes 2019 Shuffled

````
ScienceData$Condition.shuffle <- shuffle(ScienceData$Condition)
gf_histogram(~Games, data=ScienceData, fill="darkorange", color "brown4", binwidth=1) %>%
  gf_facet_grid(Condition.shuffle~.) %>%
  gf_vline(xintercept = ~mean, data=favstats(Games~Condition.shuffle, data=ScienceData), color="black")
````

* which of the following DGPs might account for the difference in means across the shuffled conditions?
  * randomness
  * we were the DGP
* 4 shuffles: why does Be Science do better in the upper left?
  * randomness
* what statistic could we use to summarize each shuffle?
  * statistic = something we calculate based on a sample
  * b<sub>1</sub>
* a **sampling distribution** is a distribution of sample statistics, or estimates
* any sample statistic can have a sampling distribution
* in a sampling distributions, all samples have to be samples of the same size

### Distribution Triad: What Distribution do Sample Statistics (Estimates) Come From?
* sampling distribution = imaginary distribution made up of all samples of size n and all the Y-bars of those samples
* not a particular number of samples; an infinitely large number of samples

### Draw Pictures
* what kind of questions require model of DGP vs. sampling distribution?
* don't assume any of these have the same shape
* mean of sample is not necessarily the same as mean of population
  * sampling variation
  * but can be used as a parameter estimate
  * gives a since of how off it can be
* sample distribution provides context for interpreting single score
* sample distribution provides context for interpreting sample statistic (parameter estimate)
  * although we collected a distribution of scores, we only have one mean
  * we need to know what distribution that mean comes from
* **sampling distribution is a model of the distribution of estimates**
* any parameter estimate can be thought of as coming from a sampling distribution of all possible samples *of the same size* that could have been drawn from the same DGP
* could there be a sampling distribution of b<sub>1</sub>?
  * yes, it's statistic/estimate
  * we want to know about that sampling distribution for context

## Modeling Sampling Distributions
* with R
  * simulation (`rnorm`)
  * randomization (`shuffle`)
  * bootstrapping (`resample`)
* mathematical models

### Constructing a Sampling Distribution of b<sub>1</sub>
* what does this code do?

````
outcome <- rnorm(n=10, mean=100, sd=15)
group <- rep(letters[1:2], each = 5)
study <- data.frame(group,outcome)
````
* `rnorm`: mathematically construct a normal distribution with a mean of 100 and sd of 15 and randomly take 10 numbers from that distribution
* `rep`: way to make a categorical variable (for simulations), makes 5 of A's and B's each
* random sampling of numbers and random pairing of numbers with a grouping variable
  * simulating a distribution
  * asking 'if'

````
gf_histogram(~outcome, data=study, color="darkgreen") %>%
  gf_facet_grid(group~.) %>%
  gf_refine(scale_x_continuous(limits=c(50,150))) %>%
  gf_vline(xintercept = ~mean, data=favstats(outcome~group, data=study), color="blue")
lm(outcome~group, data=study)
supernova(lm(outcome~group, data=study))
````

* trying to simulate b<sub>1</sub>
  * simulate a sample of data
  * simulate it into two groups
  * fit the model
  * calculate the mean of each group
  * difference between those group means is b<sub>1</sub>
* what happens if I run this code again?
  * different random numbers every time will result in different distributions
  * blue vertical line (mean of distribution) is at a different value each time
  * different b<sub>1</sub> each time
* why does Group A do better in 3 of the 4 simulations
  * randomness
  
* add a line of code to get b<sub>1</sub>
````
outcome <- rnorm(n=10, mean=100, sd=15)
group <- rep(letters[1:2], each = 5)
study <- data.frame(group,outcome)
b1(outcome~group, data=study)
````
  * gives the value of b<sub>1</sub>
  * every time you run it, you will get a different b<sub>1</sub>
