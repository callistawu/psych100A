# Lecture 16 (Week 8, Wednesday)

## Analyzing ScienceData: A practical application of sampling distributions
Which distribution did b<sub>1</sub> come from? Could it have come from a DGP with a β<sub>1</sub> = 0?

### Four Ways of Creating Sampling Distributionos
* simulation
* randomization
* bootstrapping
* mathematical models

Let's use simulation to answer this question.
* to simulate: N = 80, 40 in each group
* assume sample come from normal DGP, mean = Grand Mean; SD = b<sub>0</sub>, β<sub>1</sub> = 0

Distribution of Games: Assume Normal?
* M = 3.83, SD = 1.52

Simulate a Single Random Sample
* if I make a histogram of Games.sim, will it be a sampling distribution?
  * no
  * sampling statistic: b<sub>1</sub>
  * we only have one b<sub>1</sub>, one sample
  * we would need 1,000 b<sub>1</sub>s to have a sampling distribution

Simulate sampling distribution of b<sub>1</sub>
* what will be the shape of this sampling distribution? what will be the center? what will be the spread?
  * shape: normal
  * center: 0
  * spread: you don't know - this is why we're making the sampling distribution
* we make sampling distributions because we don't knoow the spread and want to know the probability
* will the mean of this sampling distribution tell us the mean of the DGP?
  * yes, it should be centered at the mean of the DGP
  * no, it won't necessarily be centered at the mean of the DGP
