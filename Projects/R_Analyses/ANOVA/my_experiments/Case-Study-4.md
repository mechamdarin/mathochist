---
title: "Case Study 4 SP/RM [1,1]"
output: 
  html_document:
    theme: cerulean
    keep_md: true
    toc: true
    toc_float: true
    code_folding: hide
---




# NCAA March Madness... in July



## Background

Due to the outbreak of Coronavirus, professional sports were cancelled. Many people were saddened by this news including myself. In order to make up for this lack of sports in my life, I decided to use this experiment to fill that void. For this experiment, I will be shooting socks into a laundry basket. Could I be using an actual basketball hoop and basketball? Probably, but where's the fun in that? The information below will hopefully clarify what exactly I am doing in this experiment. 

* Units - Folded pairs of socks

* Treatments - Distance (10 feet and 15 feet) and Handedness (Left and Right)

* Response - Number of shots made (out of 5)



## Model

This experiment will use the following model:

$$
Y_\text{ijk} = \mu + \alpha_i + \beta_\text{ij} + \gamma_k + (\alpha\gamma)_\text{ik} + \epsilon_\text{ijk}
$$

For this model:

* $Y_\text{ijk}$ represents each individual observation (number of shots made)

* $\mu$ represents the overall mean of the experiment

* $\alpha_i$ represents the distance at which the shot was made. In this case, it will be 10 feet and 15 feet.

* $\beta_\text{ij}$ represents individuals shooting. I will be recruiting some of my friends to aid in this experiment.

* $\gamma_k$ represents the hand that the individual uses to shoot the basket (one handed shots only for simplicity).

* $(\alpha\gamma)_\text{ik}$ represents the interaction of the distance at which the shot was made and the hand that was used to shoot the basket.

* $\epsilon_\text{ijk}$ represents the residual error for each observation


## Hypotheses
1. The first hypothesis has to do with the distance. We want to see if the distance at which shots are made has a significant effect on the number of shots made.

$$
H_0: \alpha_\text{10 feet} = \alpha_\text{15 feet} = 0
$$
$$
H_a: \alpha_i \neq 0
$$



2. The second hypothesis has to do with the handedness. Once again, we are seeing if this factor has a significant effect on the number of shots made.


$$
H_0: \gamma_\text{Left Hand} = \gamma_\text{Right Hand} = 0
$$

$$
H_a: \gamma_k \neq 0
$$



3. The third and last hypothesis has to do with the interaction of the two factors above. 


$$
H_0: \alpha_\text{10 feet}\gamma_\text{Left Hand} = \alpha_\text{10 feet}\gamma_\text{Right Hand} = ... = 0
$$


$$
H_a: (\alpha\gamma)_\text{ik} \neq 0 
$$


The significance level used for this study is **0.05**

## Experimental Protocol

1. Gather the materials. Those materials are: a wire basket, folded pairs of socks (you're going to need 5), some way to measure the distance, some way to mark the distance, and a pencil/paper to record results.

2. Set up the experiment by placing the wire basket on a coffee table or some sort of low, elevated surface. 

3. Measure the distances and mark them using some sort of marker. I will be using duct tape for this.

4. Randomly assign distances to each individual. For this, I will assign a number to each individual. Using a random number generator, I will assign each individual to a distance group. 

5. Using the same sort of process, develop a shot order. Be sure to account for handedness in the shot order. I will be treating the right and left hand of an individual as separate entities.  

6. Shoot your shots and record the number of those made. 



### Sources of Variation

* Miscounts - It is possible that the person counting the shots could mess up and forget to count one. To deal with this, we will be using a whiteboard and a tally mark system for each "cell." 

* Size of socks - It is possible that the size of the folded pair of socks could mess something up. To counter this, I will be using the same size socks for each shot (Adidas low cut socks).


## Data 


```r
sock <- read_csv("../../../Data/SockBall.csv")
sock$Distance <- factor(sock$Distance)
sock$Individual <- factor(sock$Individual)
sock$Hand <- factor(sock$Hand)
sock.aov <- aov(ShotsMade ~ Distance*Hand + Individual, data = sock, contrasts = list(Distance = contr.sum, Hand = contr.sum, Individual = contr.sum))
pander(sock, caption = "The Data")
```


------------------------------------------
 Distance   Individual   Hand   ShotsMade 
---------- ------------ ------ -----------
    10          I         L         2     

    10          I         R         3     

    10          II        L         1     

    10          II        R         1     

    10         III        L         1     

    10         III        R         4     

    15          IV        L         2     

    15          IV        R         2     

    15          V         L         3     

    15          V         R         4     

    15          VI        L         2     

    15          VI        R         3     

    10          I         L         3     

    10          I         R         5     

    10          II        L         2     

    10          II        R         3     

    10         III        L         2     

    10         III        R         3     

    15          IV        L         0     

    15          IV        R         4     

    15          V         L         2     

    15          V         R         5     

    15          VI        L         3     

    15          VI        R         2     
------------------------------------------

Table: The Data

## Test


```r
pander(summary(sock.aov), caption = "SP/RM [1,1] Test Results")
```


---------------------------------------------------------------------
      &nbsp;         Df    Sum Sq    Mean Sq     F value     Pr(>F)  
------------------- ---- ---------- ---------- ----------- ----------
   **Distance**      1     0.1667     0.1667     0.1684      0.687   

     **Hand**        1     10.67      10.67       10.78     0.004683 

  **Individual**     4     9.167      2.292       2.316      0.1018  

 **Distance:Hand**   1    4.93e-30   4.93e-30   4.982e-30      1     

   **Residuals**     16    15.83      0.9896       NA          NA    
---------------------------------------------------------------------

Table: SP/RM [1,1] Test Results

For a Split Plot/Repeated Measures Design, the $p$-value for the between blocks factor is calculated differently than normal. It uses the Mean Squares value for *blocks* as opposed to residuals. The $p$-value that is obtained using this correction is **0.08814629**. While different than the $p$-value in the table, it is still not significant at the 0.05 level. 

## Visuals 


```r
palette(c("firebrick", "chartreuse"))
boxplot(ShotsMade ~ Distance, data = sock, main = "Effect of Distance on Shots Made", xlab = "Distance (in feet)", ylab = "Shots Made (out of 5)", col = palette())
```

![](Case-Study-4_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```r
boxplot(ShotsMade ~ Hand, data = sock, main = "Effect of Handedness on Shots Made", xlab = "Hand Used", ylab = "Shots Made (out of 5)", col = palette())
```

![](Case-Study-4_files/figure-html/unnamed-chunk-4-2.png)<!-- -->

```r
interaction.plot(sock$Distance, sock$Hand, sock$ShotsMade)
```

![](Case-Study-4_files/figure-html/unnamed-chunk-4-3.png)<!-- -->

```r
interaction.plot(sock$Hand, sock$Distance, sock$ShotsMade)
```

![](Case-Study-4_files/figure-html/unnamed-chunk-4-4.png)<!-- -->

## Checking Assumptions


```r
par(mfrow = c(1,2))
plot(sock.aov, which = 1)
qqPlot(sock.aov$residuals, id = FALSE)
```

![](Case-Study-4_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

## Conclusion and Analysis

At the 0.05 level, the only null hypothesis that is rejected is that of the Hand factor. There is sufficient evidence to conclude that which hand is used has an effect on how many shots are made. The boxplot shows evidence of this. It shows two distributions that appear to be stochastically different. The one for distance on the other hand shows two distributions that have quite a bit of overlap. Thus showing that distance is indeed not significant. The conclusion regarding the interaction is supported when we look at the two interaction plots above. Those lines couldn't be more parallel. The fact that they are parallel suggests that there is *not* an interaction between the Distance and Hand factors. This test seems to be pretty solid considering the state of the diagnostic plots above. The QQ plot shows some curvature, but it does stay within the boundary curves. So, it should be fine to believe the results of this test. If you're going to have a shooting contest with your friends and/or family, be sure to use your dominant side so that you get the upper hand.   
