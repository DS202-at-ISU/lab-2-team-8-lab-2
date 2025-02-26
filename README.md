
<!-- README.md is generated from README.Rmd. Please edit the README.Rmd file -->

# Lab report \#1

Follow the instructions posted at
<https://ds202-at-isu.github.io/labs.html> for the lab assignment. The
work is meant to be finished during the lab time, but you have time
until Monday evening to polish things.

Include your answers in this document (Rmd file). Make sure that it
knits properly (into the md file). Upload both the Rmd and the md file
to your repository.

All submissions to the github repo will be automatically uploaded for
grading once the due date is passed. Submit a link to your repository on
Canvas (only one submission per team) to signal to the instructors that
you are done with your submission.

Step 1

``` r
library(classdata)
head(ames)
```

    ##    Parcel ID                       Address             Style
    ## 1 0903202160      1024 RIDGEWOOD AVE, AMES 1 1/2 Story Frame
    ## 2 0907428215 4503 TWAIN CIR UNIT 105, AMES     1 Story Frame
    ## 3 0909428070        2030 MCCARTHY RD, AMES     1 Story Frame
    ## 4 0923203160         3404 EMERALD DR, AMES     1 Story Frame
    ## 5 0520440010       4507 EVEREST  AVE, AMES              <NA>
    ## 6 0907275030       4512 HEMINGWAY DR, AMES     2 Story Frame
    ##                        Occupancy  Sale Date Sale Price Multi Sale YearBuilt
    ## 1 Single-Family / Owner Occupied 2022-08-12     181900       <NA>      1940
    ## 2                    Condominium 2022-08-04     127100       <NA>      2006
    ## 3 Single-Family / Owner Occupied 2022-08-15          0       <NA>      1951
    ## 4                      Townhouse 2022-08-09     245000       <NA>      1997
    ## 5                           <NA> 2022-08-03     449664       <NA>        NA
    ## 6 Single-Family / Owner Occupied 2022-08-16     368000       <NA>      1996
    ##   Acres TotalLivingArea (sf) Bedrooms FinishedBsmtArea (sf) LotArea(sf)  AC
    ## 1 0.109                 1030        2                    NA        4740 Yes
    ## 2 0.027                  771        1                    NA        1181 Yes
    ## 3 0.321                 1456        3                  1261       14000 Yes
    ## 4 0.103                 1289        4                   890        4500 Yes
    ## 5 0.287                   NA       NA                    NA       12493  No
    ## 6 0.494                 2223        4                    NA       21533 Yes
    ##   FirePlace              Neighborhood
    ## 1       Yes       (28) Res: Brookside
    ## 2        No    (55) Res: Dakota Ridge
    ## 3        No        (32) Res: Crawford
    ## 4        No        (31) Res: Mitchell
    ## 5        No (19) Res: North Ridge Hei
    ## 6       Yes   (37) Res: College Creek

The variables in the dataset are Parcel ID, Address, Style, Occupancy,
Sale Date, Sale Price, Multi Sale, YearBuilt, Acreas, TotalLivingArea
(sf), Bedrooms, FinishedBsmtArea (sf), LotArea(sf), AC, FirePlace, and
Neighborhood. The variables types include chrs, factors, dates, and
doubles.

The variable meanings:

Parcel ID: character with ID.

Address: property address in Ames, IA.

Style: factor variable detailing the type of housing.

Occupancy: factor variable of type of housing.

Sale Date: date of sale.

Sale Price: sales price (in US dollar).

Multi Sale: logical value: was this sale part of a package?

YearBuilt: integer value: year in which the house was built.

Acres: acres of the lot.

TotalLivingArea (sf): total living area in square feet.

Bedrooms: number of bedrooms.

FinishedBsmtArea (sf): total area of the finished basement in square
feet.

LotArea(sf): total lot area in square feet.

AC: logical value: does the property have an AC?

FirePlace: logical value: does the property have an fireplace?

Neighborhood: factor variable - levels indicate neighborhood area in
Ames.

Possible ranges for each numerical variable:

Date: 2017 to 2022

Sale Price: 0 to 20,500,000

YearBuilt: 2017 to 2022

Acres: 12

TotalLivingArea (sf): 6000

Bedrooms: 10

FinishedBsmtArea (sf): 6500

LotArea(sf): 500000

Step 2

Acres, TotalLivingArea (sf), Bedrooms, and YearBuilt are likely
variables that influence Sales Price.

Step 3

``` r
summary(ames$`Sale Price`)
```

    ##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
    ##        0        0   170900  1017479   280000 20500000

The range of Sales Price is \$20,500,000.

``` r1
library(ggplot2)

ggplot(ames, aes(x = ames$`Sale Price`)) + 
  geom_histogram(binwidth = 500000) + 
  labs(title = "Histogram of Sales Price") +
  xlab("Sales Price")
```

The distribution of sales prices is right skewed with a few major
outliers. There appear to be a lot of values where the Sales Price is 0.

Step 4

Nina’s Work:

My chosen variable is Bedrooms. The possible range of this variable is
0-10. Most values lie around 2-5, and has a few outliers.

This follows the general pattern, and doesn’t describe any oddities
discussed earlier.

Christopher’s Work:

Jamey’s Work: I made a scatter plot with x = TotalLivingArea and y =
Sale Price. But, it was incredibly zoomed out so I limited the cartesian
coordinate range. There seems to be a positive correlation between Total
Living Area and Sale Price based on the graph, although I would probably
have to make a correlation matrix to confirm.

Ryan’s Work:

``` r
library(dplyr)
ames_new <- ames %>% filter(YearBuilt != 0)
summary(ames_new$`YearBuilt`)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    1880    1956    1978    1976    2002    2022

After removing null values, the range is 1880 to 2022.

``` r
library(ggplot2)
library(dplyr)
ggplot(ames_new, aes(x = YearBuilt, y = ames_new$`Sale Price`)) +
  geom_point() +
  labs(title = "Year Built vs. Sale Price")
```

    ## Warning: Use of `` ames_new$`Sale Price` `` is discouraged.
    ## ℹ Use `Sale Price` instead.

![](README_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
ames_new <- ames_new %>% filter(ames_new$`Sale Price` != 0)
ggplot(ames_new, aes(x = YearBuilt, y = ames_new$`Sale Price`)) +
  geom_point() +
  labs(title = "Year Built vs. Sale Price")
```

    ## Warning: Use of `` ames_new$`Sale Price` `` is discouraged.
    ## ℹ Use `Sale Price` instead.

![](README_files/figure-gfm/unnamed-chunk-5-2.png)<!-- -->
