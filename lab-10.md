## Load packages and data

    library(tidyverse) 
    library(tidymodels)
    library(openintro)

## Exercise 1

The slope is 0.067, and intercept is 3.88. R-squared is 0.035; adjusted
R-squared is 0.033

score = 0.067(bty\_avg) + 3.88

    ?evals

    m_bty <-lm(score ~ bty_avg, data = evals)
    summary(m_bty)

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

## Exercise 2 to 9

1.  score = 3.95 + 0.03(bty\_avg) − 0.18(gender) +
    0.08(bty\_avg\*gender). R-squared = 0.071, adjusted R-squared =
    0.065

2.  intercept (3.95) represents the predicted teaching evaluation score
    for a female instructor (when gender = 0) whose beauty average
    (bty\_avg) is 0.

3.  6.5% variance in score is explained by m\_bty\_gen

4.  equation for male professors: score = 0.11(bty\_avg) + 3.77

5.  equation for female professors: score = 0.03(bty\_avg) + 3.95. When
    two professors receive the same beauty rating below 2.25, female
    professors tend to have higher evaluation scores. But when the
    beauty score exceeds 2.25, male professors tend to have higher
    evaluation scores.

6.  Female professors: the slope is 0.03. For each one-unit increase in
    beauty rating, female professors’ evaluation scores are predicted to
    increase by 0.03 points. This relationship is weak and not
    statistically significant (p = 0.2), meaning beauty doesn’t strongly
    predict evaluation scores for females.

Male professors: the slope is 0.11. For each one-unit increase in beauty
rating, male professors’ evaluation scores are predicted to increase by
0.11 points. This relationship is stronger than that of female
professors, but still not significant (p = 0.23).

1.  the adjusted R-squared increases by 0.032 from the m\_bty model,
    this suggests that adding gender to the model, particularly the
    interaction term between gender and beauty, helps to explain more of
    the variability in course evaluation scores.

2.  The slope of bty\_avg decreases drastically when gender is added to
    the model. This means that bty\_avg alone is no longer a significant
    predictor of score, when other predictors are controlled (i.e.,
    gender and its interaction with bty\_avg).

<!-- -->

    m_bty_gen <-lm(score ~ bty_avg * gender, data = evals)
    summary(m_bty_gen)

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg * gender, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8084 -0.3828  0.0903  0.4037  0.9211 
    ## 
    ## Coefficients:
    ##                    Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)         3.95006    0.11800  33.475   <2e-16 ***
    ## bty_avg             0.03064    0.02400   1.277   0.2024    
    ## gendermale         -0.18351    0.15349  -1.196   0.2325    
    ## bty_avg:gendermale  0.07962    0.03247   2.452   0.0146 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5258 on 459 degrees of freedom
    ## Multiple R-squared:  0.07129,    Adjusted R-squared:  0.06522 
    ## F-statistic: 11.74 on 3 and 459 DF,  p-value: 1.997e-07

## Exercise 10

1.  score = 4.1 + 0.04(bty\_avg) − 0.02(tenure track) − 0.41(tenured) −
    0.03(bty\_avg*tenure track) + 0.07(bty\_avg*tenured)

The linear model predicts course evaluation scores based on professors’
beauty ratings and rank, including interactions. Teaching professors
with a beauty score of 0 have an average evaluation score of 4.1. There
is a significant effect of rank on evaluation score, but I am not sure
which group is set as the reference by r, so I set teaching professor as
the reference group and run the model again. The results suggest that
there is a significant effect of rank on score such that teaching
professors tend to have higher score than tenured professors (p =
0.007), whereas there is no significant difference of score between
teaching and tenure track professor. The interaction between bty\_avg
and tenuredTeach contrast is also significant (p = 0.01), meaning that
the evaluation scores differ based on beauty rating (bty\_avg) and
professor’s rank (teaching or tenured).

    m_bty_rank <-lm(score ~ bty_avg * rank, data = evals)
    summary(m_bty_rank)

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg * rank, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8584 -0.3882  0.1211  0.4054  1.0062 
    ## 
    ## Coefficients:
    ##                          Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)               4.09811    0.14959  27.395   <2e-16 ***
    ## bty_avg                   0.04171    0.03138   1.329   0.1844    
    ## ranktenure track         -0.01885    0.23044  -0.082   0.9349    
    ## ranktenured              -0.40910    0.18218  -2.246   0.0252 *  
    ## bty_avg:ranktenure track -0.02640    0.04632  -0.570   0.5690    
    ## bty_avg:ranktenured       0.06586    0.03922   1.679   0.0938 .  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5305 on 457 degrees of freedom
    ## Multiple R-squared:  0.05871,    Adjusted R-squared:  0.04841 
    ## F-statistic: 5.701 on 5 and 457 DF,  p-value: 4.089e-05

    # setting the teaching professor as the reference group
    evals$tenuredTeach <- dplyr::recode(evals$rank, 
                           "teaching" = 0,
                           "tenure track" = 0,
                           "tenured" = 1)

    evals$ttrackTeach <- dplyr::recode(evals$rank, 
                           "teaching" = 0,
                           "tenure track" = 1,
                           "tenured" = 0)

    m_bty_rank1 <-lm(score ~ bty_avg * tenuredTeach, data = evals)
    summary(m_bty_rank1)

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg * tenuredTeach, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.9285 -0.3882  0.1335  0.4082  1.0062 
    ## 
    ## Coefficients:
    ##                      Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)           4.10847    0.11368  36.140  < 2e-16 ***
    ## bty_avg               0.02323    0.02290   1.014  0.31089    
    ## tenuredTeach         -0.41946    0.15422  -2.720  0.00678 ** 
    ## bty_avg:tenuredTeach  0.08434    0.03287   2.566  0.01062 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5317 on 459 degrees of freedom
    ## Multiple R-squared:  0.05033,    Adjusted R-squared:  0.04412 
    ## F-statistic: 8.108 on 3 and 459 DF,  p-value: 2.847e-05

    m_bty_rank2 <-lm(score ~ bty_avg * ttrackTeach, data = evals)
    summary(m_bty_rank2)

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg * ttrackTeach, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8584 -0.3810  0.1146  0.4089  0.9436 
    ## 
    ## Coefficients:
    ##                     Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)          3.81002    0.08525  44.694  < 2e-16 ***
    ## bty_avg              0.08695    0.01886   4.612 5.19e-06 ***
    ## ttrackTeach          0.26924    0.19571   1.376   0.1696    
    ## bty_avg:ttrackTeach -0.07164    0.03909  -1.833   0.0675 .  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5332 on 459 degrees of freedom
    ## Multiple R-squared:  0.04508,    Adjusted R-squared:  0.03883 
    ## F-statistic: 7.222 on 3 and 459 DF,  p-value: 9.596e-05

## Exercise 11 to 13

1.  the worst predictor is probably cls\_students I tried to think of
    all the possibilities but just cannot justify that the number of
    students can influence teacher’s evaluation. Number of a class is
    more about course structure or for administrative purpose, and
    students likely don’t associate directly with how they rate the
    professor.

2.  score = 0.0002(cls\_students) + 4.16 The relationship is extremely
    weak and not significant. Number of students in class do not have
    effect on evaluation scores (p = 0.58).

3.  I would not include cls\_did\_eval if cls\_studnets and
    cls\_perc\_eval are already included, because the interaction
    between cls\_studnets and cls\_perc\_eval is cls\_did\_eval, and
    including another cls\_did\_eval would be redundant.

<!-- -->

    m_students <-lm(score ~ cls_students, data = evals)
    summary(m_students)

    ## 
    ## Call:
    ## lm(formula = score ~ cls_students, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8666 -0.3677  0.1281  0.4300  0.8336 
    ## 
    ## Coefficients:
    ##               Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  4.1643491  0.0314034 132.608   <2e-16 ***
    ## cls_students 0.0001881  0.0003373   0.558    0.577    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5443 on 461 degrees of freedom
    ## Multiple R-squared:  0.0006744,  Adjusted R-squared:  -0.001493 
    ## F-statistic: 0.3111 on 1 and 461 DF,  p-value: 0.5773

## Excercise 14 to 18

1.  score = 3.60 − 0.12(tenure track) − 0.03(tenured) + 0.22(minority) +
    0.18(gender) − 0.01(age) + 0.01(cls\_perc\_eval) +
    0.51(cls\_credit) + 0.06(bty\_avg)
2.  A slope of 0.22 of minority means that when the a professor is not
    minority (vs. monirty), their evaluation score will increase by 0.22
    unit. A slope of -0.01 of age means that for every one year a
    professor ages, their evaluation score will decrease by 0.01 unit.
3.  a young, male, not minority, attractive professor who have high
    proportion of students responding to his one credit course tends to
    have the highest evaluation score.
4.  No, the characteristics in \#17 seem to suggest that a very specific
    social group of professors is favored (young white males), and the
    sample was collected in Austin, TX. I would probably imagine the
    preference to be different in other states, e.g., California,
    Hawaii, or New York, where schools hire more diverse employees and
    students might have different preferences of professors (or even no
    preference for social group at all) due to increased exposure. Also
    even after fitting the model, the r-squared of 14.3% is still not
    very large, suggesting there are more variables that weren’t tested
    but could explain the variance in evaluation score.

<!-- -->

    # fit everything except for the cls_did_eval
    m_full <- lm(score ~ rank + ethnicity + gender + language + age + 
                   cls_perc_eval * cls_students + cls_level + cls_profs + 
                   cls_credits + bty_avg, data = evals)
    summary(m_full)

    ## 
    ## Call:
    ## lm(formula = score ~ rank + ethnicity + gender + language + age + 
    ##     cls_perc_eval * cls_students + cls_level + cls_profs + cls_credits + 
    ##     bty_avg, data = evals)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1.83665 -0.31377  0.08559  0.35655  1.08091 
    ## 
    ## Coefficients:
    ##                              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)                 3.604e+00  2.615e-01  13.780  < 2e-16 ***
    ## ranktenure track           -1.023e-01  8.234e-02  -1.242 0.214915    
    ## ranktenured                -4.441e-02  6.526e-02  -0.681 0.496514    
    ## ethnicitynot minority       1.838e-01  7.770e-02   2.366 0.018423 *  
    ## gendermale                  1.813e-01  5.170e-02   3.507 0.000499 ***
    ## languagenon-english        -1.298e-01  1.082e-01  -1.200 0.230850    
    ## age                        -6.568e-03  3.087e-03  -2.128 0.033900 *  
    ## cls_perc_eval               4.676e-03  2.106e-03   2.220 0.026904 *  
    ## cls_students               -9.486e-04  1.973e-03  -0.481 0.630832    
    ## cls_levelupper              1.038e-02  5.681e-02   0.183 0.855083    
    ## cls_profssingle            -5.001e-03  5.162e-02  -0.097 0.922860    
    ## cls_creditsone credit       5.063e-01  1.171e-01   4.323  1.9e-05 ***
    ## bty_avg                     6.092e-02  1.669e-02   3.650 0.000293 ***
    ## cls_perc_eval:cls_students  2.237e-05  3.112e-05   0.719 0.472698    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5043 on 449 degrees of freedom
    ## Multiple R-squared:  0.1645, Adjusted R-squared:  0.1403 
    ## F-statistic: 6.799 on 13 and 449 DF,  p-value: 5.372e-12

    # remove cls_profs, cls_level, language, cls_students as they do not explain significantly more variance in the model

    m_full <- lm(score ~ rank + ethnicity + gender + age + 
                   cls_perc_eval + cls_credits + bty_avg, data = evals)
    summary(m_full)

    ## 
    ## Call:
    ## lm(formula = score ~ rank + ethnicity + gender + age + cls_perc_eval + 
    ##     cls_credits + bty_avg, data = evals)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1.84113 -0.31628  0.07816  0.35598  1.07330 
    ## 
    ## Coefficients:
    ##                        Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)            3.597655   0.234496  15.342  < 2e-16 ***
    ## ranktenure track      -0.124279   0.079805  -1.557 0.120100    
    ## ranktenured           -0.033075   0.064058  -0.516 0.605875    
    ## ethnicitynot minority  0.219760   0.072453   3.033 0.002559 ** 
    ## gendermale             0.179925   0.050919   3.534 0.000452 ***
    ## age                   -0.007378   0.003033  -2.432 0.015388 *  
    ## cls_perc_eval          0.005008   0.001441   3.475 0.000560 ***
    ## cls_creditsone credit  0.512099   0.111203   4.605 5.36e-06 ***
    ## bty_avg                0.064487   0.016397   3.933 9.70e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5035 on 454 degrees of freedom
    ## Multiple R-squared:  0.1577, Adjusted R-squared:  0.1429 
    ## F-statistic: 10.63 on 8 and 454 DF,  p-value: 1.005e-13
