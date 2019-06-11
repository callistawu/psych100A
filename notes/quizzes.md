## Quiz 5

* most likely explanation for the different shapes of distributions: **sampling variation**
  * there are different participants in each condition and so no two samples will be exactly the same
* dividing participants into two equal groups
  * `TetrisData$Distress.Group <- ntile(TetrisData$Distress, 2)`
* how many variables are represented in faceted histogram: 2
* determine how many participants in TetrisData data frame reported Distress scores of less than 5
  * `LowDistress <- filter(TetrisData, Distress < 5)`
  * `tally(LowDistress)`
* find the mean
  * `mean(TetrisData$Intrusions_1_7)`
* histogram shows distribution of participants' ratings of Distress
  * count (y-axis) = number of participants
* create a new categorical variable and add to TetrisData data frame
  * `TetrisData$Condition.Factor <- factor(TetrisData$Condition)`
* for a boxplot, smaller rectangle = less variability among scores
* data frame
  * rows = participants
  * columns = variables
* boxplot
  * IQR: rectangle
  * outliers: dots
* word equation: Intrusions_1_7 = Condition + other stuff
  * outcome variable = quantitative
  * explanatory variable = categorical
  * other stuff = variation unexplained
* what differs between a density histogram and a histogram?
  * scale of the y-axis
* IQR = Q3 - Q1
* scatterplot
  * represent the model post_Horror = mean + other stuff with a horizontal line at the mean of post_Horror
* in what sense is the mean the middle of the distribution?
  * the absolute value of the sum of the deviations above the mean is equal to the absolute value of the sum of the deviations below the mean
* fit the empty model for Intrusions_0 - 3.319 is:
  * the mean of Intrusions_0
  * the model prediction for a participant's score on Intrusions_0
  * b<sub>0</sub>
* the distribution of residuals from the empty model would have the same shape as the distribution of Intrusions_1_7
* for the empty model for Intrusions_1_7, every participant will have the same predicted score for Intrusions_1_7
* a **parameter** cannot be calculated from the TetrisData dataset
* b<sub>0</sub> can be calculated from the TetrisData dataset
* `lm()` output:
  * variance = mean sq
* standard deviation = roughly the average residual from the mean
* larger standard deviation = distribution is wider and more variable
* if we remove a participant from the sample, minimum, mean, and sum of squares would all change
* null model is called "empty" because it doesn't contain any explanatory variables
* z-score tells you each individual's standing relative to their particular distribution
* what can we conclude?
  * P(X>8) = P(Z>1.212) = 0.1128
  * the probability of the next randomly drawn observation being greater than 8 is approximately 0.11
* what deviation represents the error for each participant from the Condition.model?
  * `lm(Games~Condition, data=ScienceData)`
  * the deviation of each participant's Games score from the mean Games score for their Condition
* a **residual** is the difference between a data point's value and its predicted value under a model
* use `lm()` function to calculate value of b<sub>0</sub>
  * impossible to know how much variation is explained with this information
* model Games = Condition + Other Stuff is represented in GLM notation by Y<sub>i</sub> = b<sub>0</sub> + b<sub>1</sub>X<sub>i</sub> + e<sub>i</sub>
  * which part of this model will generate a prediction for the next randomly chosen observation from either the Be Scientist or the Do Science Condition?
  * b<sub>0</sub> + b<sub>1</sub>X<sub>i</sub>
* interpretation of PRE:
  * .4154 of the SS total in the Empty model is explained by the Condition model
* if we fit a different model, using Age to predict Games, what would likely stay the same?
  * SS total because total variation for the same outcome variable doesn't change
* which of these statistics would help us evaluate which of the two models explains more variation?
  * both SS error and F
* Y<sub>i</sub> = b<sub>0</sub> + b<sub>1</sub>X<sub>i</sub> + e<sub>i</sub>
  * 2 parameters estimated in this model
* regression model
  * the sum of the residuals around the regression line is always equal to 0
* SS model on a jitter plot
  * vertical distance between empty model and complex model
  * b<sub>1</sub> is represented by the distance between the predicted values of both complex models
* which visualization would be helpful in exploring the relationship between Condition and Games?
  * faceted histogram, box plot, scatter plot
* **F ratio** indicates how much we have reduced error compared with the empty model per degree of freedom spent
* the **null model** quantifies how much total variation exists in the outcome variable that has yet to be explained
* empty model and complex model should have the same SS total (sum of squares)
* evaluate the effect of distracted on total
  * fit the model total = distracted + other stuff
  * `lm(total~distracted, data=LaptopData)`
  * create a sampling distribution for the b<sub>1</sub> statistic
* probability that a chosen participant will have a score that is greater than or equal to 0.65
  * `tally(~total >= 0.65, data=LaptopData)`
* you plan to take a new random sample of n=38 participants. which distribution would you use to calculate the probability that the sample's average score on total would be less than 0.32?
  * the sampling distribution of means
* the distribution of the DGP can be normal, even if the sample looks skewed
* sampling distribution of shuffled b<sub>1</sub>s
  * `SDoB1.shuffle <- do(1000)*b1(total~shuffle(condition), data=LaptopData)`
  * `gf_histogram(~b1, data=SDoB1.shuffle)`
  * the sampling distribution is centered at 0 because the distribution was created from total scores being paired randomly with condition, so we would expect there to be no effect of condition
* b<sub>1</sub> is represented by the difference between mean of the no-view condition and the mean of the view condition
* we can create a sampling distribution for: PRE, b<sub>0</sub>, F
* `predict()` function gives one predicted score for each possible score on distracted
  * `lm(total~distracted, data=LaptopData)`
* SS error: vertical distance between individual data point and regression line
* a **sampling distribution** represents a distribution of sample statistics from which our sample statistic could have come
* the standard deviation of the sampling distribution should be smaller than the standard deviation of distracted in the LaptopData study
* what does the output represent?
  * `distracted.stats <- favstats(LaptopData$distracted)`
  * `SDoM.sim <- do(1000)*mean(rnorm(n=38, mean=distracted.stats$mean, sd=distracted.stats$sd))`
  * `head(SDoM.sim)`
  * means of simulated samples of n=38
* the residuals above and below the regression line should add up to 0
* z-score = 1.9
  * participant scored 1.9 standard deviations above the mean score on total for all participants
* GLM notation for a three-group model
  * Y<sub>i</sub> = b<sub>0</sub> + b<sub>1</sub>X<sub>1i</sub> + b<sub>2</sub>X<sub>2i</sub> + e<sub>i</sub>
