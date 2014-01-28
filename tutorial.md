*Explain what is a variable and data structure.*

Vector
------

A vector is a collection of objects (e.g., numbers, text, true/false values).
The command (or function) `c` combines objects to create a vector.

    x <- c(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

An easier way to generate a sequence of numbers is

    x <- 1:10

Operations
----------

Many operations work directly on vectors, applying the operation on each
element of the vectors involved.

    y <- 10:1
    z <- x + y
    a <- 2 * x

Basic operations are `+`, `-`, `*`, `/`, and `^`. For example,

    y <- x^2    # Replaces old value of y

**Exercise.** Write R code to generate the first 100 odd numbers.

**Solution.** `2 * 1:100 - 1`

Functions
---------

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

Help
----

R has a help system you can call on any function:

    ?rnorm

It tells you what the function is, how it is used, what its parameters mean,
and additional information (including examples).

Histograms
----------

We can quickly verify that these random numbers come from a normal distribution
by plotting a histogram:

    x <- rnorm(10000, mean=100, sd=25)
    hist(x)

**Exercise.** Plot a histogram of the normal distribution (10,000 numbers)
with a mean of 0 and a standard deviation of 1.

**Solution.** hist(rnorm(10000))

Summary statistics
------------------

Given a vector of numbers, we can also get some summary statistics:

    summary(x)

Or specific quantiles, like the 2.5% and 97.5% quantiles:

    quantile(x, prob=c(0.025, 0.975))

Other useful functions you can use are `sum`, `mean`, `median`, `var`,
`min`, and `max`.

User-defined functions
----------------------

You can create your own functions in R. Writing functions is a nice way to
modularize your code so that the same function can be called more than once
and you don't have to keep writing the same piece of code over and over.
Top me, code duplication is the greatest evil in software development.
This is because duplicated code is difficult to maintain---if you make a change
in one piece, you have to find all the others to make the same change.
With a function, you make the chance once, and everyone who calls the function
automatically gets the change.

To write a function in R:

    stddev <- function(x) { sqrt(var(x)) }

Functions could span multiple lines if necessary, but the function returns
the value of the last statement. We'll practice creating functions in the
exercises.

**Exercise.** Write a function `se` to calculate the stdardard error of x.

**Solution.** `se <- function(x) { sd(x) / sqrt(length(x)) }`

As mentioned, functions may have several parameters, some of which may be
optional. For example:

    jitter <- function(x, amount=1) { x + rnorm(length(x), mean=0, sd=amount) }

Sampling
--------

Sometimes you want to take a random sample from your data, either with
or without replacement. For example,

    sample(x, size=10, replace=T)    # T is True

takes a subsample. To randomize your data, don't specify a size:

    sample(x, replace=T)

One may want to take thousands of such samples, calculate some statistic,
and examine the distribution of such statistic. This is known as bootstrapping.
To replicate an operation many times and get the result of each operation
as an element of a vector, use `replicate`:

    replicate(10, mean(sample(x, replace=T)))

**Exercise.** Write a function that computes the 95% bootstrap
confidence interval of the mean for `x`.

**Solution.**
`ci <- function(x) { quantile(replicate(10000, mean(sample(x, replace=T))), prob=c(0.025, 0.975)) }`

Data frame
----------

We've been working with vectors so far, but another important data structure
in R is the data frame. A data frame is like a table, with rows and columns,
and the columns are often named.

R comes with many built-in data sets, which often come as data frames.
See the built-in data sets:

    data()

Let's look at the data frame `trees`:

    trees

*Explain structure.*

We can access each column as a vector by specifying the header name after
the data frame variable name:

    trees$Girth

We can also access each row as a one-row data frame using bracket notation:

    trees[1,]    # First number is the row, empty columns means grab all

Instead of giving it a row index, we can also specify a conditional expression:

    trees[trees$Height > 75,]

**Exercise.** Write a function to calculate the mean Volume of x,
a data frame that conforms to `trees`, with a Girth less than `max_girth`.

**Solution.** `vol <- function(x, max_girth) { mean(x[x$Girth < max_girth,]$Volume) }`

Reading data
------------

Usually, your data will be in the form of a table in a file. It could be an
Excel file, which you'll need to export as a CSV file.

**Exercise.** Create a CSV file with headers `Age` (in years) and `Height`
(in inches) and fill it up with some made-up data. Call the file `height.csv`.

To read this file in R as a data frame:

    data <- read.csv('height.csv')
