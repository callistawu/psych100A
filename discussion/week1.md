# Week 1 Discussion

## Reviewing R
### Recreate a data table
````
age <- c(25,33,35,38,48,55,55,55,56,64)
fired <- c("no", "no", "no", "no", "no", "no", "yes", "yes", "no", "yes")
westvaco <- data.frame(age, fired)
westvaco
````
* `westvaco <- data.frame(fired, age)` just changes the order of the columns
* `westvaco$age` specifically calls the **age** variable from the **westvaco** data frame
* spacing doesn't matter, but punctuation does


```
str(westvaco)
```
* structure: tells us number of variables, what types of variables
* **fire** is a categorical variable
* useful for knowing what variables you're working with and what kind of variables they are


### Visualizing the relationship between age and fired
* can't make a histogram with the variable **fire** because it's categorical
* the `~` operator tells you what the independent and dependent variables are (e.g. x is a function of y)

````
gf_histogram( ~age, data = westvaco, binwidth = 10)
gf_point(age ~ fired, data = westvaco)
gf_boxplot(age ~ fired, data = westvaco)
````

* the `%>%` (piping) operator links two functions together
* `gf_facet_grid` separates into groups
````
gf_histogram( ~age, data = westvaco, binwidth = 10)
gf_facet_grid(fired~.)
````
