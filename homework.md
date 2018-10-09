HW4
================
Malvika Mitra
8th Oct 2018

``` r
suppressPackageStartupMessages(library(tidyverse)) # to supress messages after library calls
```

    ## Warning: package 'readr' was built under R version 3.3.2

``` r
suppressPackageStartupMessages(library(ggplot2))
suppressPackageStartupMessages(library(gapminder))
```

    ## Warning: package 'gapminder' was built under R version 3.3.2

``` r
library(knitr)
```

# DATA RESHAPING:

\#Data Reshaping is about changing the way data is organized into rows
and columns. Most of the time data processing is done by taking the
input data as a data frame. It is easy to extract data from the rows and
columns of a data frame but there are situations when we need the data
frame in a format that is different from format in which we received it.
Functions like gather() and spread() from **tidyr** reshape the rows to
columns in a data frame.

## Activity \#2

Make a tibble with one row per year and columns for life expectancy for
two or more countries.

Use knitr::kable() to make this table look pretty in your rendered
homework.

Take advantage of this new data shape to scatterplot life expectancy for
one country against that of
another.

``` r
my_gap<-gapminder %>% #making a new dataframe and saving it                         in the variable my_gap.
  group_by(year) %>% 
  filter((country=="Canada"| country=="Algeria")) 
my_gap
```

    ## # A tibble: 24 x 6
    ## # Groups:   year [12]
    ##    country continent  year lifeExp      pop gdpPercap
    ##    <fct>   <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Algeria Africa     1952    43.1  9279525     2449.
    ##  2 Algeria Africa     1957    45.7 10270856     3014.
    ##  3 Algeria Africa     1962    48.3 11000948     2551.
    ##  4 Algeria Africa     1967    51.4 12760499     3247.
    ##  5 Algeria Africa     1972    54.5 14760787     4183.
    ##  6 Algeria Africa     1977    58.0 17152804     4910.
    ##  7 Algeria Africa     1982    61.4 20033753     5745.
    ##  8 Algeria Africa     1987    65.8 23254956     5681.
    ##  9 Algeria Africa     1992    67.7 26298373     5023.
    ## 10 Algeria Africa     1997    69.2 29072015     4797.
    ## # ... with 14 more rows

``` r
g<-tibble(year=my_gap$year,lf=my_gap$lifeExp,country=my_gap$country)  #making a tibble
knitr::kable(g)
```

| year |     lf | country |
| ---: | -----: | :------ |
| 1952 | 43.077 | Algeria |
| 1957 | 45.685 | Algeria |
| 1962 | 48.303 | Algeria |
| 1967 | 51.407 | Algeria |
| 1972 | 54.518 | Algeria |
| 1977 | 58.014 | Algeria |
| 1982 | 61.368 | Algeria |
| 1987 | 65.799 | Algeria |
| 1992 | 67.744 | Algeria |
| 1997 | 69.152 | Algeria |
| 2002 | 70.994 | Algeria |
| 2007 | 72.301 | Algeria |
| 1952 | 68.750 | Canada  |
| 1957 | 69.960 | Canada  |
| 1962 | 71.300 | Canada  |
| 1967 | 72.130 | Canada  |
| 1972 | 72.880 | Canada  |
| 1977 | 74.210 | Canada  |
| 1982 | 75.760 | Canada  |
| 1987 | 76.860 | Canada  |
| 1992 | 77.950 | Canada  |
| 1997 | 78.610 | Canada  |
| 2002 | 79.770 | Canada  |
| 2007 | 80.653 | Canada  |

``` r
gapminder %>% 
  filter((country=="Canada"| country=="Algeria")) %>% 
ggplot(aes(year,lifeExp))+
  geom_point(aes(color=country))+
  ggtitle("      ScatterPlot of LifeExp")+
  xlab("Year")+
  ylab("LifeExp")
```

![](homework_files/figure-gfm/unnamed-chunk-1-1.png)<!-- --> \# Output:
Filtered the Gapminder data according to requirements and saved it
my\_gap variable. \#Then made a tibble out of the columns of my\_gap.
\#Knitted the table and finally made the scatter plot of the lifeExp of
Canada ana Algeria over the years. \#The graph shows that the lifeExp of
Canada is higher than that of Algeria.

## Activity \#3

\#Compute some measure of life expectancy (mean? median? min? max?) for
all possible combinations of continent and year. Reshape that to have
one row per year and one variable for each continent. Or the other way
around: one row per continent and one variable per year. \#Use
knitr::kable() to make these tables look pretty in your rendered
homework. \#Is there a plot that is easier to make with the data in this
shape versis the usual form? If so (or you think so), try it\! Reflect.
