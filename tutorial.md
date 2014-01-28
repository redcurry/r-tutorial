*Explain what is a variable and data structure.*

A vector is a collection of objects (e.g., numbers, text, true/false values).
The command (or function) `c` combines objects to create a vector.

    x <- c(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

An easier way to generate a sequence of numbers is

    x <- 1:10

Many operations work directly on vectors, applying the operation on each
element of the vectors involved.

    y <- 10:1
    z <- x + y
    a <- 2 * x

Basic operations are `+`, `-`, `*`, `/`, and `^`. For example,

    y <- x^2    # Replaces old value of y

**Exercise.*** Write R code to generate the first 100 odd numbers.

Functions in R are similar to mathematical functions. A function applies
an operation to its parameters, if any, and returns a new value.

    length(x)
    log(x)         # Natural logarithm
    y <- sin(x)
    rnorm(10)

The `rnorm` function returns a vector of random numbers, taken from
a normal distribution, where you specify the number of elements in the vector.
Functions in R may also take in optional parameters. For example,
the rnorm function uses a normal distribution with a mean of 0
and standard deviation of 1. You may change these values with optional
parameters:

    rnorm(10, mean=100, sd=25)    # You can specify parameters by name

We can quickly verify that these random numbers come from a normal distribution
by plotting a histogram:

    x <- rnorm(10000, mean=100, sd=25)
    hist(x)

Given a vector of numbers, we can also get some summary statistics:

    summary(x)

Or specific quantiles, like the 2.5% and 97.5% quantiles:

    quantile(x, prob=c(0.025, 0.975))

If `x` was the result of bootstrapping, this would be your 95% bootstrap
confidence interval.

Other useful functions you can apply are `sum`, `mean`, `median`, `var`,
`min`, and `max`.


