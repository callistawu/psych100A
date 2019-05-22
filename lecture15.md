# Lecture 15 (Week 8, Monday)

## Sampling Distributions to Confidence Intervals

### Constructing a Sampling Distribution of b<sub>1</sub>s
````
SDoB1
SDoB1 <- do(1000)* {
  outcome <- rnorm(n=10, mean=100, sd=15)
  group <- rep(letters[1:2], each = 5)
  study <- data.frame(group,outcome)
  b1(outcome~group, data=study)
}
gf_dhistogram(~result, data=SDoB1, fill="cyan", color="dodgerblue")%>%
gf_refine(scale_x_continuous(limits=c(-40,40)))

tally(~result > 5, data=SDoB1, format="proportion")
````
* look at `head(SDoB1)` - what does each of these numbers represent?
  * the group difference between group a and b for a sample of n=10 drawn from the DGP
  * `do()` command creates a data frame

Sampling distribution of b<sub>1</sub>: What is "count" the count of?
* b<sub>1</sub>: mean difference between the mean scores in the a group (5) and the mean scores in the b group (b)
  * take average of the a's, take average of the b's
  * take the difference of those
  * result: increment from group a and b (b<sub>1</sub>)
  * repeat 1000 times
* why do you think this distribution is centered at 0?
  * there's no difference between these groups
  * didn't discover anything about the world because it's completely made up
  * but we discovered how much spread there is in the distribution
    * each of these is an estimate
  * standard error of the estimate is how variable is that estimate
* how to calculate PRE for one of these samples
  * fit model first using 'lm(outcome~group, data=study)'
  * `supernova()`
  * each sample would have a different PRE due to sampling variation
* could you create a sampling distribution of PRE?
  * yes, PRE is a **sample statistic** (anything you can calculate for a sample)
  * sampling distribution is a distribution for sample statistics

Casting the Question as Model Comparison
* what are the chances that our sample estimate b<sub>1</sub> could have come from a DGP with β<sub>1</sub> = 0?

If we change do(1000) to do(500)
* what effect will it have on the probability of randomly selecting a sample with a b<sub>1</sub> > 5?
* doesn't change the standard deviation of the sampling distribution
* width doesn't change; a little smoother
* can see this quantitatively with `tally()` or `favstats()`

If we change n=10 to n=40, each=20
* what effect will it have on probability of randomly selecting a sample with a b<sub>1</sub> > 5?
* shrinks standard error, narrower
* lower probability

If we change the mean of DGP from 100 to 200
* what effect will it have on probability of randomly selecting a sample with a b<sub>1</sub> > 5?
* stay the same
* takes DGP and shifts it a little

If we change SD of DGP from 15 to 30
* what effect will it have on probability of randomly selecting a sample with a b<sub>1</sub> > 5?
* increase

Which distribution should I use: DGP or a sampling distribution?
> I'm making a new ride for a theme park. It's not safe for anyone less than 60 inches tall to ride on it. What percentage of park attendees will be ineligible to ride?
* population distribution (DGP)
* don't want a sampling distribution because we're not asking about the probability of a sample statistic
* asking about probability of an individual person who attends the park
* question is asking what percentage of park attendees are less than 60 inches tall?

> In order to get state approval for my ride, I need to show that the average weight of the 10 people that fit into each car will be less than 150 pounds 99.9% of the time.
* sampling distribution
* looking for probability of a sample statistic
