---
layout: lesson
root: ../..
title: Writing R functions
---





> ### Learning Objectives {.objectives}
>
> * Why write functions
> * How to define a function
> * Defining graphing functions
> * Scope and global variables
> * Conditional statements
> * `match.arg`


### Why?

There are two main reasons to write R functions.

- Avoid repeated code
- More readable code

As an example, consider this code to convert 65 degrees Fahrenheit to
Celsius.


~~~{.r}
cel <- (65 - 32)*5/9
~~~

If you then want to convert 100 degrees F, you'll have to retype all
of that. And the code itself doesn't really explain it's purpose.


~~~{.r}
f2c <-
    function(fahrenheit)
{
    celsius <- (fahrenheit - 32)*5/9
    return(celsius)
}
~~~

The definition of a function has three parts:

- `function()`, containing any _arguments_ (in other words, parameters or inputs) that the
  function takes
- The body of the function (the bit that is executed when the function
  is called)
- The assignment of the function to an object; in this case we've
  called it `f2c`

Having executed the above code, you'll note that there's now an object in
your R workspace called `f2c`. (Try `ls()`.)

You can use the function like any other R function:


~~~{.r}
f2c(65)
~~~



~~~{.output}
[1] 18.33333

~~~

Note that you can even give it a vector of Fahrenheit temperatures.


~~~{.r}
f2c(c(100, 212, 32, -40))
~~~



~~~{.output}
[1]  37.77778 100.00000   0.00000 -40.00000

~~~

### Implicit return value


The function definition could actually be simplified. In R functions,
an explicit `return` statement is not needed; the function will
_return_ the value of the last statement, so we could write:


~~~{.r}
f2c <-
    function(fahrenheit)
{
    (fahrenheit - 32)*5/9
}
~~~

And, actually, the curly braces aren't needed when the function has
just one statement. We could have written:


~~~{.r}
f2c <-
    function(fahrenheit)
    (fahrenheit - 32)*5/9
~~~


> ### Challenge {.challenge}
>
> Write the opposite function, for converting from Celsius to
> Fahrenheit. Test that it works.


### Functions for plotting

Functions are particularly useful when making graphs. You'll often
want to make the same sort of graph multiple times, for example, a
scatterplot of `lifeExp` vs `gdpPercap` for each of several different
years. Rather than repeat the code multiple times, write a function
that does the work and then call it several times.

Let's reload the `gapminder` data, as before.


~~~{.r}
gapminder <- read.csv("~/Desktop/gapminder.csv")
~~~



Here's a function to make a plot for a particular year.


~~~{.r}
plot_year <-
    function(year=2007, data=gapminder)
{
    library(dplyr)
    library(ggplot2)

    the_year <- year
    gm_year <- filter(data, year==the_year)

    ggplot(gm_year, aes(y=lifeExp, x=gdpPercap)) +
        geom_point() + scale_x_log10()
}
~~~

The function returns the ggplot object. You could add further
enhancements after the fact.


~~~{.r}
plot_year(1952) + aes(color=continent) + ggtitle(1952)
~~~

<img src="fig/functions-use_plot_year-1.png" title="plot of chunk use_plot_year" alt="plot of chunk use_plot_year" style="display: block; margin: auto;" />

Note that I passed the data as an argument and gave each argument a
default value.

> ### Challenge {.challenge}
>
> Write a function that makes a plot of `lifeExp` vs `gdpPercap` across
> years, for a selected country.



~~~{.r}
plot_country <-
    function(country="China", data=gapminder)
{
    library(dplyr)
    library(ggplot2)

    the_country <- country
    gm_country <- filter(data, country==the_country)

    p <- ggplot(gm_country, aes(y=lifeExp, x=gdpPercap)) +
        geom_point()

    p
}
~~~


### Scope

- variables defined within a function are destroyed on exit.
- if function refers to a variable that hasn't been defined locally,
  look outside to global environment.
- things are more tricky for functions defined within functions, but
  maybe we'll skip that.



### Conditional statements



~~~{.r}
plot_year <-
    function(year=2007, data=gapminder, add_curve=TRUE)
{
    library(dplyr)
    library(ggplot2)

    the_year <- year
    gm_year <- filter(data, year==the_year)

    p <- ggplot(gm_year, aes(y=lifeExp, x=gdpPercap)) +
        geom_point() + scale_x_log10()

    if(add_curve)
        p <- p + geom_smooth(method="loess")

    p
}
~~~


Maybe also include `include_se`?

> ### Challenge: {.challenge}
>
> Add an option to your `plot_country` function, to use `geom_line()`
> as well as `geom_point()`.


~~~{.r}
plot_country <-
    function(country="China", data=gapminder, add_line=FALSE)
{
    library(dplyr)
    library(ggplot2)

    the_country <- country
    gm_country <- filter(data, country==the_country)

    p <- ggplot(gm_country, aes(y=lifeExp, x=gdpPercap)) +
        geom_point()

    if(add_line)
        p <- p + geom_line()

    p
}
~~~


### Multiple-choice arguments

Add `method` argument, to allow that you might use either `"loess"` or
`"lm"` for the curve.


~~~{.r}
plot_year <-
    function(year=2007, data=gapminder, add_curve=TRUE, method="loess")
{
    library(dplyr)
    library(ggplot2)

    the_year <- year
    gm_year <- filter(data, year==the_year)

    p <- ggplot(gm_year, aes(y=lifeExp, x=gdpPercap)) +
        geom_point() + scale_x_log10()

    if(add_curve)
        p <- p + geom_smooth(method=method)

    p
}
~~~

Can be helpful to give multiple choices. You could then use
`match.arg()` to ensure that the selected choice is allowable.


~~~{.r}
plot_year <-
    function(year=2007, data=gapminder, curve=c("none", "loess", "lm"))
{
    curve <- match.arg(curve)

    library(dplyr)
    library(ggplot2)

    the_year <- year
    gm_year <- filter(data, year==the_year)

    p <- ggplot(gm_year, aes(y=lifeExp, x=gdpPercap)) +
        geom_point() + scale_x_log10()

    if(curve != "none")
        p <- p + geom_smooth(method=curve)

    p
}
~~~

> ### Challenge {.challenge}
>
> Modify your function to take an argument `type` with possible values
> `"points"`, `"lines"`, or `"both"`, indicating whether to use
> `geom_point()`, `geom_line()`, or both.


### The `...` argument

You might also want to be able to pass `se` (taking values `TRUE` or
`FALSE`).

We could just go back to `add_curve` but then also include an argument
`...` which is passed to `geom_smooth`, to cover each of `method` and `se`.


~~~{.r}
plot_year <-
    function(year=2007, data=gapminder, add_curve=FALSE, ...)
{
    curve <- match.arg(curve)

    library(dplyr)
    library(ggplot2)

    the_year <- year
    gm_year <- filter(data, year==the_year)

    p <- ggplot(gm_year, aes(y=lifeExp, x=gdpPercap)) +
        geom_point() + scale_x_log10()

    if(add_curve)
        p <- p + geom_smooth(...)

    p
}
~~~

Problem here: if they use `add_curve=TRUE`, they need to also indicate
a method; otherwise they'll get an error. **(Or will they?)**

### Resources

- See the
  [chapter on functions](http://adv-r.had.co.nz/Functions.html) in
  [Hadley Wickham](http://had.co.nz/)'s
  [Advanced R book](http://adv-r.had.co.nz/), also available on
  [paper](http://www.amazon.com/exec/obidos/ASIN/1466586966/7210-20).
