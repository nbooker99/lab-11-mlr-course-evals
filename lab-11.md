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

> Fit a linear model (one you have fit before): m_bty_gen, predicting
> average professor evaluation score based on average beauty rating
> (bty_avg) and gender. Write the linear model, and note the R-squared
> and the adjusted R-squared.

``` r
m_bty_gen <- summary(lm(score ~ bty_avg + gender, data = evals))
m_bty_gen
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg + gender, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8305 -0.3625  0.1055  0.4213  0.9314 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  3.74734    0.08466  44.266  < 2e-16 ***
    ## bty_avg      0.07416    0.01625   4.563 6.48e-06 ***
    ## gendermale   0.17239    0.05022   3.433 0.000652 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5287 on 460 degrees of freedom
    ## Multiple R-squared:  0.05912,    Adjusted R-squared:  0.05503 
    ## F-statistic: 14.45 on 2 and 460 DF,  p-value: 8.177e-07

score = 3.75 + 0.07 x bty_avg + 0.17 x gendermale + error

R-squared = .06

Adjusted R-squared = .06

## Exercise 3

> Interpret the slope and intercept of m_bty_gen in context of the data.

The intercept, 3.74, represents the predicted evaluation score for a
professor who has an average beauty rating of 0 and is female.

The slopes indicate that, when controlling for gender (i.e., when
comparing professors of the same gender), a 1-unit increase in average
beauty score is associated with a .07 point increase in evaluation
scores and that, when controlling for average beauty rating, male
professors, on average, have a an evaluation score that is .17 points
greater than the average female professor.

## Exercise 4

> What percent of the variability in score is explained by the model
> m_bty_gen.

Since this is a multiple regression, I would refer to the adjusted
R-squared, which indicates that the model explains about 5.5% of
variance in evaluation scores.

## Exercise 5

> What is the equation of the line corresponding to just male
> professors?

score = 3.75 + 0.07 x bty_avg + 0.17 x (1) + error

score = 3.92 + 0.07 x bty_avg + error

## Exercise 6

> For two professors who received the same beauty rating, which gender
> tends to have the higher course evaluation score?

The male professor. This is indicated by the positive coefficient for
the “gendermale” term in the model which also includes beauty rating as
a predictor.

## Exercise 7

> How does the relationship between beauty and evaluation score vary
> between male and female professors?

We cannot know from the current model whether the relatationship between
beauty and evaluation score varies by gender. To answer that question,
we would need a regression model with an interaction term (i.e.,
gendermale\*bty_avg). The current model can only tell us the
relationship between beauty and evaluation scores when statistically
controlling for gender.

“The current model assumes that the relationship between beauty rating
and evaluation scores is the same for both genders \[…\] The current
model forces both gender groups to have the same slope (0.07), even
though the true slopes might differ,” (Claude.ai).

## Exercise 8

> How do the adjusted R-squared values of m_bty_gen and m_bty compare?
> What does this tell us about how useful gender is in explaining the
> variability in evaluation scores when we already have information on
> the beauty score of the professor.

Adjusted R-squared for m_bty is .03 while the adjusted R-squared for
m_bty_gender is .06. This indicates that adding gender out model doubles
the amount of variance in evaluation scores explained by the model. In
other words, it is useful to know about the gender of the professor if
we want to predict evaluation scores, even if we already know about the
professors beauty score.

## Exercise 9
