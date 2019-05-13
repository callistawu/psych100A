# Lecture 4 (Week 2, Wednesday)

## Exploring Variation in Data
Always start by looking at the distributions of variables: **center, shape, spread, and weird stuff.**

* Package: `okcupiddata`
* Data frame: `profiles`

Find out about the data frame `profiles`. How many observations and variables does the profiles data frame have?
````
str(profiles)
````
* 59946 observations,  22 variables


## Cleaning Data
Examine the distribution of **age**.
````
gf_histogram(~ age, data=profiles, fill="orange")
````

Why do you think this distribution has the shape it does?
* unimodal
* not normal
* skewed right

Run a favstats() on **age**.
````
favstats(~age, data=profiles)
````
* What do you notice? Were there any clues in the histogram?
  * The max age is 110. The minimum is 18. The median is 30 (middle score in whole distribution).
* Suggest some ways to figure out what's going on, and how to fix it.

````
profiles <- filter(profiles, age<100)
favstats(~age, data=profiles)
gf_histogram(~age, data=profiles, fill="purple")
````

## The Five Number Summary
````
favstats(~ age, data=profiles)
````
* Plot the five number summary for age on a number line - to scale
* min - Q1 - median - Q3 - max
* Why are the quartiles not equally spaced?
  * the intervals contain the same number of values
* Sketch the boxplot of this distribution

## Pay Attention to Level of Measurement
````
gf_bar(~ bar, data=profiles, fill="orange")
````
* looks just like a histogram, but produced using a different method
* shape distribution doesn't make sense for a bar graph

## Explaining Variation
* In the profiles data frame, does Sex explain Height?
  * fewer females than males
* Working Definition: Knowing someone's value on the explanatory variable helps you make a better guess about their value on the outcome variable.
