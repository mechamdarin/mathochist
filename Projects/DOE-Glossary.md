---
title: "DOE Glossary"
output: 
  html_document:
    theme: cerulean
    keep_md: true
    toc: true
    toc_float: true
    code_folding: hide
---



#### Instructions

This glossary is to be a *log of your knowledge and understanding* of key words, principles, and methods within the design of experiments (DOE) field.  It is to be filled in as the semester progresses.  *It is not* a place to copy and paste definitions from other sources or to copy them word for word.  *You should not* fill in a glossary entry immediately after reading a definition in the textbook.  *You should* read and study the textbook and then wait a few hours (or a day) and then fill in related entries of the glossary *in your own words*, as if you were teaching this concept to another person.  

To really know something you must build and create your own knowledge map. The purpose of this glossary is to 1) help you clarify your understanding of important DOE concepts 2) convince yourself that your really know them 3) help you retain that knowledge, and 4) be a resource to your future self.

You are free to add more terms to this glossary and to add bulletlists or subsections to terms as you build your knowledge map.

----

#### Terms

**ANOVA**

* Analysis of Variance - compares variation between each of the sample means and within each sample

* R - name.aov <- aov(response ~ factor, data = TheData, contrasts = list(factor = contr.sum))


**ANCOVA**  

* Analysis of Covariance 

* ANCOVA is used when your nuisance variable is continuous. In other words, when you can't pin down your nuisance variable

* It is similar to the equal slopes model of Multiple Linear Regression

* R - name.lm <- lm(response ~ explanatory*"dummy" variable, data = TheData, contrasts = list("dummy" variable = contr.sum))

**Balanced Design**  

* leads to easier analysis

* larger statistical power

* more robust procedures

* Use table() to check for balanced data (equal amounts in each combination)


**BF Basic Factorial Design**  

* CR Completely Randomized  

* refers to structure of data, how you analyze it, etc.

* BF[x] - x is the number of factors of interest (there can be interactions too)

* [Case Study BF[1]](R_Analyses/ANOVA/my_experiments/Case-Study-1.md)

* [Case Study BF[2]](R_Analyses/ANOVA/my_experiments/Case-Study-2.md)


**Bias**

* Prevents observations from being equal to the true values

* pushes every measurement in the same direction resulting in distortion


**Blinding**

* "Hiding" parts of the experimentation from certain individuals involved in the study

* Blinding helps prevent bias in the study

* Examples of blinding can be found in drug trials with placebos and the placebo effect

* With blinding, the subject does not know what they are getting themselves into

* With double blinding, neither the subject nor the person who's conducting the experiment knows


**Blocking**  

* This is a means to deal with the nuisances that you can "pin down"

* Meaning the nuisances that are discrete. 

* Individuals are a common block

* In a way, this is a way of acknowledging the variability while not considering it in calculations

* It reduces the amount of variability that would otherwise be found in the residuals


**CB Complete Block Design**  

* This is a basic model that involves blocks

* Essentially, it is a One-Way ANOVA that includes some sort of block

* R - name.aov <- aov(Response ~ Block + Treatment, data = TheData, contrasts = list(Treatment = contr.sum))

* We focus on the Treatment in this design

* The block is not of as much concern

* [Case Study CB[1]](R_Analyses/ANOVA/my_experiments/Case-Study-3.md)


**Comparison / Contrast**  

* This allows for a different look of your data.

* By using this, you can make certain comparisons within your data. 

* R - (YOU NEED emmeans package)

* Establish model

* NameMeans <- emmeans(model, "Factor")

* NameMeans to display means of that group along with other numbers including Confidence Intervals

* NameContrasts <- contrast(NameMeans, list(Name = c(Coefficients), ...), adjust = "none")

* NameContrasts

* The coefficients are all dependent on you

* Remember order of factors when setting these up


**Conditions / Treatments**  

* This is what you are interested in and what you want to control in the experiment

* This could be any number of things

* In Case Study 1, it was the design of the airplane


**Confidence Interval**  

* An inferential procedure that takes sample data and gives a general idea of where the parameter could lie.

* Confidence Intervals typically have three different widths: 90%, 95%, and 99%.

* Changing the confidence level can increase or decrease the width of the interval


**Confounding**  

* Simply put, it is confusing the impact of one variable for something else

* One way to mitigate that is to incorporate that "something else" into the study in some way (blocking for example)


**Control**

* This is the status quo

* Everything needs to be as "normal" as possible so as not to introduce some other form of variability


**Crossing**  

* Combining factors in every possible way

* With three factors, you end up with 4 interactions because of the three way interaction and the lower two way interactions


**Decomposition**

* Manually calculating the ANOVA table using Excel

* By doing this, you can see the effects of a factor right off the bat

* General rule of thumb: Average - sum of outside effects

* It is a bit of a journey, but it is worth it. You can see what is done behind the scenes in R


**Degrees of Freedom**

* Referred to as the number of "free numbers"

* You can only spend so many before you start to see the same thing over and over again

* The degrees of freedom follows that general rule of thumb that was mentioned earlier.

* Certain studies will have different ways of calculating degrees of freedom (shortcuts, really)

* The degrees of freedom will always add up to the number of observations


**Effects**

* This is a numerical representation of the impact that each factor has on the response.

* This can either be found through manual decomposition or by using dummy.coef(name.aov)/name.aov$residuals

* Average - sum of outside effects


**Experimental Content**  

* Response (Measurement) - This is obviously what you are interested in. This is what you are measuring. In Case Study 2, it was the size of the splash zone of a water balloon.  

* Conditions: These are the different treatments. In Case Study 2, it was the Size of the balloons and the Distance at which the balloons were thrown. This is what we change to see its effect on the response.  

* Material - In a way, this is seen as the object that produces your response. In Case Study 2, it was the water balloons.


**Experimental Study**

* This is a study where you are implementing treatments upon subjects and collecting some sort of measurements from them.

* These *can* be difficult to execute when they involve human subjects 


**Experimental Unit**

* subjects

* To elaborate, these are the items that the treatment is being imposed upon

* The paper in Case Study 1 was the Experimental Unit. It was assigned to different treatment groups (Different plane designs) and a response was collected as a result of their efforts (distance thrown).


**F-Ratio**

* ratio of variances - between group variability divided by within group variability

* A large $F$ value leads to a small $p$-value and a small $F$ value leads to a larger $p$-value. This is a general rule of thumb, but it isn't necessarily law. Best to double check.


**Factor**

* Universal - the same across every study (Benchmark and Residuals)

* Structural - these tend to change depending on the study (treatments, interactions, etc.)

**Factor Levels**

* These are subdivisions of the factor

* For Case Study 4, it was the distances and the handedness

**Factor Structure**

* Factors can either be in another factor, or they can be outside of another factor

* This can also help pinpoint how you want to lay out your study

* By looking at the factor structure, you can also figure out which type of study you want to do (specifically how you want to lay it out).

**Fixed Factor**  

* If the factor levels are controllable, then the factor is fixed. 

**Fisher Assumptions**  

* Additive Model - This refers to the idea that observed values are a sum of all effects involved. Best way to check this is do a decomposition and have a section where you add up the effects. If you get the observed values, WOOHOO

* Constant Means - The observed values that have the same factors involved should have the same true value  

* Zero Mean Errors  - The average of your observed values will get closer and closer to your true value

* Constant Variance Errors  - The variance found among the errors is constant throughout the data. You want to have values that are the same distance from the fitted values. Best way to check this is with a residuals versus fitted plot. R - plot(name.aov, which = 1)

* Normal Errors  - The residuals follow a normal distribution. Best way to check this is with a QQ plot. I like the qqPlot(name.aov$residuals) function found in library(car)

* Independent Errors  - There is no pattern in the residuals

**Fractional Factorial**

* This is a method of condensation while still capturing information about your factors of interest.

* Be mindful of confounding with this particular design

**Full Factorial**

* "Going all out" 

* This is also known as a BF[3] design

* This involves a total of 4 interaction terms

* R - name.aov <- aov(Response ~ Factor1 * Factor2 * Factor3, data = TheData...)


**Imputation**  

* This is a practice that is used to deal with missing data 

* It can be dangerous if used improperly

* Possible bias can be introduced


**Interaction**

* This is the result of crossing factors

* You want to have all possible treatment combinations

* If the $p$-value for this is significant, it should be interpreted first and be the only one

* The * operator gives the highest level interaction and all below it

* Otherwise, it can be written out using : between the factors of interest.

**Kinds of Variability**  

* Planned Systematic - This variability is desired. It can help determine what factors should be implemented into the study.

* Chancelike - This variability can also be classified as "behind the scenes" variability. Mistakes in the experimentation itself can lead to this

* Unplanned Systematic  - This variability tends to come from a lack of planning. For example, if you didn't consider individuals in the initial design, that can seriously screw things up in the experimentation. Best way to deal with this, get rid of the nuisance by blocking (most common way of dealing with it).

**LS Latin Square Design**  

* Latin Squares has two nuisance factors and one factor of interest

* These factors all have to have the same number of levels

* There is only factor of interest in this specific design. Thus, no interaction

* R - name.aov <- aov(Response ~ Block1 + Block2 + Treatment, data = TheData, contrasts = list(Block1 = contr.sum....))

* The "aov" portions *can* be replaced by "lm", but that is personal preference


**Mean Squares**

* This shows the average variability for that specific item. 

* It can be also called the variance


**Measurement Classification** (Steven's Four Types)  

* Nominal  - This is a category that items can be separated into. This category has no order to it. Hair and eye color are examples of this type of measurement.

* Ordinal  - This category is similar to the first, but it has order to it. The Likert scale (used in a lot of surveys) is an example of this.

* Interval - This category has numbers and a distance between them that makes sense. Weight can be an example of this

* Ratio  - Once again, there are numbers involved that have a distance between them. In the case of ratios, there is a natural zero too. 

**Multiple Comparisons Problem**  

* Family-wise error rate - If you do multiple tests without doing some kind of adjustment, you run the risk of combining the "false alarm" rate of all of those tests... Thus making the chance of getting a false alarm much higher. (In this instance, the false alarm rate is also known as $\alpha$)  

* Adjustments  - These methods are used to make one of the multiple comparison methods work. It varies based on which one you want to use (Fisher, Tukey, Bonferroni, and Scheffe).

**Nesting**  

* Think of Russian Nesting dolls, but with factors

* The observed values are the whole thing

* Each component is either inside or outside another factor

* There can be situations where all of the factors won't fit together all nice and pretty. 

* Best way to find out which factor is outside/inside of which is to draw it out and see where the rectangles can be superimposed without crossing boundaries.

**Nuisance Influence**  

* This can be seen as a lurking variable

* In a lot of studies, it can be individuals involved

* This is why blocking is so crucial. It may not be a cure-all

* If the nuisance is continuous, go to ANCOVA as opposed to a CB design. 

**Observational Study**

* No treatment is imposed upon a population, but something is noted about a population

* Depending on the situation, "people watching" applies here

**Outliers**  

* Definition  - These are values that are far from the rest of our data (below or above). They can be referred to as "loners." They're off by themselves

* Remedies  - One of the most effective ways to deal with outliers is to remove them. This can be dangerous though because it *could* lead to bias. You could compute the analysis with AND without them to see their true impact. There are certain procedures that are robust enough that they can deal with outliers. Imputation is another method and that was mentioned above.

**p-value**  

* It is the probability of witnessing that same data land to prove the null true


**Parameter**

* These numbers describe your population - $\mu$ for population mean and $\sigma$ for population standard deviation

**Population**

* The group that is pulled from. It is difficult to get information about the population. It is expensive too.

**Random Factor**  

* You are concerned about the levels present and the levels behind the scene

* It is essentially a sampling of factors from a population

**Randomization**

* a means of converting unplanned, systematic variability into planned, chancelike variability

**Response**

* measurements being made

**Reliability**

* the ability to get the same answer under similar circumstances

**Root Mean Square**

* This will often produce the variance of the factor in question

**Sample**

* A taste of what the population is like

* This breaks the population into manageable portions and can be used to make inferences about the population

* Several sampling techniques can be employed in order to reduce any sort of bias.

**Sources of Variability**  

* Conditions  - This variability is wanted because you want to see which level of your factor/s is most beneficial/detrimental to the response.

* Material  - This is not wanted... Best way to deal with it is Blocking.

* Measurement Process - Once again, not wanted. Best way to deal with it is replication and reduction of any bias. Also, CALIBRATION of measuring machinery.

**SP/RM Split Plot / Repeated Measures Design**  

* whole plot <-> between-subjects <-> between-blocks  

* subplot <-> within-subjects <-> within-blocks  

* This design involves two factors of interest, their interaction, and a block.

* R - name.aov <- aov(Response ~ BetweenBlock*WithinBlock + Block, data = TheData, ...)

* [Case Study SP/RM [1, 1]](R_Analyses/ANOVA/my_experiments/Case-Study-4.md)

**Statistic**

* These are numbers that describe your sample - $\bar{x}$ for sample mean and $s$ for sample standard deviation

**Sum of Squares**

* This value shows the total variability due to that source

* One of the first values displayed in an ANOVA table

* =sumsq(array) for Excel calculation

* This value will automatically be computed in R

**Uniformity vs. Representativeness**  

* This debate depends on what exactly you want to do

* If you want to minimize the amount of variability that you have due to individuals, then you're going for uniformity

* If you want to make stronger inferences concerning the population, then you want representativeness


**Validity**

* measure what you think you are measuring

**Variability**

* There are three sources of variability

* planned, systematic

* chance-like

* unplanned, systematic

* A good design will let you estimate the amount of variability due to each source

----
