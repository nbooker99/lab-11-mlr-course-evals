Lab 11 - Grading the professor, Pt. 2
================
Noah Booker
4/24/25

## Load packages and data

``` r
library(tidyverse) 
library(tidymodels)
library(openintro)
```

# Part 1: Simple linear regression

## Exercise 1

> Fit a linear model (one you have fit before): m_bty, predicting
> average professor evaluation score based on average beauty rating
> (bty_avg) only. Write the linear model, and note the R-squared and the
> adjusted R-squared.

``` r
m_bty <- summary(lm(score ~ bty_avg, data = evals))
m_bty
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.9246 -0.3690  0.1420  0.3977  0.9309 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  3.88034    0.07614   50.96  < 2e-16 ***
    ## bty_avg      0.06664    0.01629    4.09 5.08e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5348 on 461 degrees of freedom
    ## Multiple R-squared:  0.03502,    Adjusted R-squared:  0.03293 
    ## F-statistic: 16.73 on 1 and 461 DF,  p-value: 5.083e-05

score = 3.89 + .07 x bty_avg + error

R-squared = .04

adjusted R-squared = .03

# Part 2: Multiple linear regression

## Exercise 2

*Provide your answer here.*  
Add code chunks as needed.

``` r
# Add your R code here
```

## Additional Exercises

*Repeat the format above for additional exercises.*
