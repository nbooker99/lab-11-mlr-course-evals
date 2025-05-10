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

score = 3.89 + .07(bty_avg) + error

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

score = 3.75 + 0.07(bty_avg) + 0.17(gendermale) + error

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

score = 3.75 + 0.07(bty_avg) + 0.17(1) + error

score = 3.92 + 0.07(bty_avg) + error

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
m_bty_gender is .06. This indicates that adding gender to the model
doubles the amount of variance in evaluation scores explained by the
model. In other words, it is useful to know about the gender of the
professor if we want to predict evaluation scores, even if we already
know about the professors beauty score.

## Exercise 9

> Compare the slopes of bty_avg under the two models (m_bty and
> m_bty_gen). Has the addition of gender to the model changed the
> parameter estimate (slope) for bty_avg?

Adding gender to the model changed the slope of bty_avg from .066 to
.074. So, it slightly strengthened the slope.

## Exercise 10

> Create a new model called m_bty_rank with gender removed and rank
> added in. Write the equation of the linear model and interpret the
> slopes and intercept in context of the data.

``` r
m_bty_rank <- summary(lm(score ~ bty_avg + rank, data = evals))
m_bty_rank
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg + rank, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8713 -0.3642  0.1489  0.4103  0.9525 
    ## 
    ## Coefficients:
    ##                  Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)       3.98155    0.09078  43.860  < 2e-16 ***
    ## bty_avg           0.06783    0.01655   4.098 4.92e-05 ***
    ## ranktenure track -0.16070    0.07395  -2.173   0.0303 *  
    ## ranktenured      -0.12623    0.06266  -2.014   0.0445 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5328 on 459 degrees of freedom
    ## Multiple R-squared:  0.04652,    Adjusted R-squared:  0.04029 
    ## F-statistic: 7.465 on 3 and 459 DF,  p-value: 6.88e-05

score = 3.98 + 0.07(bty_avg) - 0.16(rank_tenure track)
-0.13(ranktenured) + error

The intercept indicates that a professor of with a 0 beauty rating who
is a teaching professor has a predicted evaluation score of 3.98.

The slope of beauty average indicates that, controlling for rank, a
1-unit increase in beauty rating is associated with a .07-unit increase
in evaluation score.

The slope of rank_tenure_track indicates that, controlling for beauty
rating and whether the professor is teaching or tenured, a tenure-track
professor has a predicted evaluation score which is .16 units less than
a teaching professor.

Similarly, the slope of rank_tenured indicates that, controlling for
beauty rating and whether the professor is teaching or tenure-track, a
tenured professor has a predicted evaluation score which is .13 units
less than a teaching professor.

# Part 3: The search for the best model

> Going forward, only consider the following variables as potential
> predictors: rank, ethnicity, gender, language, age, cls_perc_eval,
> cls_did_eval, cls_students, cls_level, cls_profs, cls_credits,
> bty_avg.

## Exercise 11

> Which variable, on its own, would you expect to be the worst predictor
> of evaluation scores? Why? Hint: Think about which variable would you
> expect to not have any association with the professor’s score.

I would expect cls_profs, the number of professors teaching sections in
course in sample (values are “single” or “multiple”), to be the worst
predictor of evaluation scores because all of the other variables seem
like they could have some effect, but this variable doesn’t seem like it
would. I don’t imagine that the fact that the professor is or is not the
only professor teaching a section of a course would significantly impact
professor evaluations.

## Exercise 12

> Check your suspicions from the previous exercise. Include the model
> output for that variable in your response.

``` r
m_bty_cls_profs <- summary(lm(score ~ cls_profs, data = evals))
m_bty_cls_profs
```

    ## 
    ## Call:
    ## lm(formula = score ~ cls_profs, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8554 -0.3846  0.1154  0.4154  0.8446 
    ## 
    ## Coefficients:
    ##                 Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)      4.18464    0.03111 134.493   <2e-16 ***
    ## cls_profssingle -0.02923    0.05343  -0.547    0.585    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5443 on 461 degrees of freedom
    ## Multiple R-squared:  0.0006486,  Adjusted R-squared:  -0.001519 
    ## F-statistic: 0.2992 on 1 and 461 DF,  p-value: 0.5847

This model seems to indicate that my suspicion that cls_profs would not
have an effect on evaluation scores was accurate. This is indicated by
the nonsignificance (p = .585) of the slope.

## Exercise 13

> Suppose you wanted to fit a full model with the variables listed
> above. If you are already going to include cls_perc_eval and
> cls_students, which variable should you not include as an additional
> predictor? Why?

I would not also include cls_did_eval because the information contained
in that variable (the number of students in the class who completed the
evaluation) is completely redundant with the combined information
provided by cls_perc_eval and cls_students. Therefore, adding
cls_did_eval to the model would not explain any additional variance in
evaluation scores.

## Exercise 14

> Fit a full model with all predictors listed above (except for the one
> you decided to exclude) in the previous question.

``` r
full_model <- summary(lm(score ~ rank + ethnicity + gender + language + age + cls_perc_eval + cls_students + cls_level + cls_profs + cls_credits + bty_avg, data = evals))
full_model
```

    ## 
    ## Call:
    ## lm(formula = score ~ rank + ethnicity + gender + language + age + 
    ##     cls_perc_eval + cls_students + cls_level + cls_profs + cls_credits + 
    ##     bty_avg, data = evals)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1.84482 -0.31367  0.08559  0.35732  1.10105 
    ## 
    ## Coefficients:
    ##                         Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)            3.5305036  0.2408200  14.660  < 2e-16 ***
    ## ranktenure track      -0.1070121  0.0820250  -1.305 0.192687    
    ## ranktenured           -0.0450371  0.0652185  -0.691 0.490199    
    ## ethnicitynot minority  0.1869649  0.0775329   2.411 0.016290 *  
    ## gendermale             0.1786166  0.0515346   3.466 0.000579 ***
    ## languagenon-english   -0.1268254  0.1080358  -1.174 0.241048    
    ## age                   -0.0066498  0.0030830  -2.157 0.031542 *  
    ## cls_perc_eval          0.0056996  0.0015514   3.674 0.000268 ***
    ## cls_students           0.0004455  0.0003585   1.243 0.214596    
    ## cls_levelupper         0.0187105  0.0555833   0.337 0.736560    
    ## cls_profssingle       -0.0085751  0.0513527  -0.167 0.867458    
    ## cls_creditsone credit  0.5087427  0.1170130   4.348  1.7e-05 ***
    ## bty_avg                0.0612651  0.0166755   3.674 0.000268 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.504 on 450 degrees of freedom
    ## Multiple R-squared:  0.1635, Adjusted R-squared:  0.1412 
    ## F-statistic: 7.331 on 12 and 450 DF,  p-value: 2.406e-12

## Exercise 15

> Using backward-selection with adjusted R-squared as the selection
> criterion, determine the best model. You do not need to show all steps
> in your answer, just the output for the final model. Also, write out
> the linear model for predicting score based on the final model you
> settle on.

``` r
full_model <- summary(lm(score ~ ethnicity + gender + language + age + cls_perc_eval + cls_students + cls_credits + bty_avg, data = evals))
full_model
```

    ## 
    ## Call:
    ## lm(formula = score ~ ethnicity + gender + language + age + cls_perc_eval + 
    ##     cls_students + cls_credits + bty_avg, data = evals)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1.89519 -0.31227  0.08596  0.37022  1.09853 
    ## 
    ## Coefficients:
    ##                         Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)            3.3863086  0.2094164  16.170  < 2e-16 ***
    ## ethnicitynot minority  0.2044482  0.0746764   2.738 0.006428 ** 
    ## gendermale             0.1768250  0.0503142   3.514 0.000485 ***
    ## languagenon-english   -0.1511723  0.1035293  -1.460 0.144930    
    ## age                   -0.0048725  0.0026073  -1.869 0.062298 .  
    ## cls_perc_eval          0.0057538  0.0015405   3.735 0.000212 ***
    ## cls_students           0.0004073  0.0003428   1.188 0.235355    
    ## cls_creditsone credit  0.5230953  0.1050306   4.980 9.03e-07 ***
    ## bty_avg                0.0618985  0.0165267   3.745 0.000203 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5028 on 454 degrees of freedom
    ## Multiple R-squared:  0.1602, Adjusted R-squared:  0.1454 
    ## F-statistic: 10.82 on 8 and 454 DF,  p-value: 5.463e-14

score = 3.39 + 0.20(ethnicitynot minority) + 0.18(gendermale) -
0.15(languagenon-english) - 0.01(age) + 0.01(cls_perc_eval) +
0.0004(cls_students) + 0.52(cls_creditsone credit) + 0.06(bty_avg) +
error

## Exercise 16

> Interpret the slopes of one numerical and one categorical predictor
> based on your final model.

The 0.01 slope for cls_perc_eval (rounded up from 0.00575) indicates
that, holding all other variables in the model constant, every 1-unit
increase in the percentage of the class that completes the evaluation is
associated with 0.01 (actually a ~0.006) unit increase in evaluation
score.

The 0.18 slope for gendermale indicates that, holding all other
variables in the model constant, a male professor is predicted to have
an evaluation score 0.18 units greater than a female professor.

## Exercise 17

> Based on your final model, describe the characteristics of a professor
> and course at University of Texas at Austin that would be associated
> with a high evaluation score.

The final model indicates that we should expect a high evaluation score
for a one-credit course with a relatively high number of students, of
which a relatively high percentage complete the evaluation, taught by a
relatively young, attractive, english-speaking, white, male professor.

## Exercise 18

> Would you be comfortable generalizing your conclusions to apply to
> professors generally (at any university)? Why or why not?

I would be hesitant to generalize the conclusion to professors at other
universities. UT Austin is a relatively large public university in the
South. It is possible that the associations observed here of some of the
characteristics of the professor (e.g., race, gender, language) with
evaluation scores may be different in northern, more elite universities
in more cosmopolitan and diverse locations.
