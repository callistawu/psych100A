# Lecture 2 (Week 1, Wednesday)

>“Robert Martin was laid off from his job at Westvaco, Inc. soon after he turned 54 years old. He sued for age discrimination.”

What kind of data would we need to evaluate this claim?

| ages of employees in one department (~~laid off~~) |
|:--------------------------------------------------:|
| 25, 33, 35, 38, 48, ~~55~~, ~~55~~, 55, 56, ~~64~~ |

What makes a data structure tidy?
* structure 1 is not tidy because each row is not an observation

### Make a data frame
* name it Westvaco
* start with two vectors, use data.frame( )
* print out the data frame

````
age <- c(25,33,35,38,48,55,55,55,56,64)
fired <- c("no", "no", "no", "no", "no", "no", "yes", "yes", "no", "yes")
westvaco <- data.frame(age,fired)
westvaco
````

### Visualize the distribution
````
gf_histogram(~ age, data=westvaco, fill="blue", binwidth=1)%>%
gf_facet_grid(fired ~.)
````
