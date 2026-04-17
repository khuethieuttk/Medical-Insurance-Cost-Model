# Medical-Insurance-Cost-Model
Predicting Medical Insurance Costs Using Multiple Linear Regression

*Model: Multiple Linear Regression*

*Languaged used: Python**
# 1. Introduction
## 1.1. Background & Motivation
In the United States, healthcare expenses continue to rise, making health insurance a major financial concern for households. In 2025, the average employer-sponsored family premium reached about $26,993 per year, placing significant economic pressure on individuals and families. Health spending accounted for roughly 17.6% of U.S. GDP in 2023, highlighting the scale of the issue at a national level. The growth in medical costs is driven by increased healthcare demand, population aging, and lifestyle-related diseases. Understanding how demographic, lifestyle, and regional factors influence insurance charges helps insurers design fair pricing systems and enables individuals to manage potential health expenses more effectively—thereby motivating the use of statistical modeling to identify key cost drivers and estimate medical charges reliably.
## 1.2 Problem Statement
Despite the availability of demographic and health data, many individuals remain unaware of the specific magnitude by which certain variables impact their insurance premiums. This project aims to address the following:
- How can we mathematically model the relationship between personal characteristics (age, sex, BMI, children, smoker, region) and medical charges?
- Which specific factors serve as the strongest predictors of high medical expenses?
- How can we optimize a predictive model to account for the skewed nature of medical cost data and ensure statistical validity?

# 2. EDA
## 2.1 Understand the variables
- **age**: age of primary beneficiary.
- **sex**: insurance contractor gender, female, male.
- **bmi**: Body mass index, providing an understanding of body weights that are relatively high or low relative to height, objective index of body weight (kg / m^2) using the ratio of height to weight, ideally 18.5 to 24.9.
- **children**: Number of children covered by health insurance / Number of dependents
- **smoker**: Smoking status (yes or no)
- **region**: The beneficiary's residential area in the US, northeast, southeast, southwest, northwest.
- **charges**: Individual medical costs billed by health insurance (target)

The 7 variables are being split into 3 groups:
- Target value: charges
- Numerical values: age, bmi, children
- Categorical values: smoker, region, sex
## 2.1 Observation
- **Smoking** is the biggest determinant causing the medical cost to rise. It means people who smoke need to pay significantly higher medical insurance costs.
- **Age, BMI and the number of children** are also factors affecting the amount of medical bills.
- People with ages ranging from 36-65 tend to pay for insurance more than people from 25-35 years old. This reflects higher health risks in older populations.
= People classified in the “Obesity II” and “Obesity III” (> 30) , that are smokers, are more likely to be charged more for medical bills. 
- People with 0-3 children often pay a higher amount of insurance cost than people with more than 3 children. However, because the proportion of the first group is much larger than that of the latter group  in the population, this conclusion is still biased.
- The effect of beneficiary’s gender and region on the charges of medical cost are ambiguous. Hence for the model below, we will exclude these factors to avoid ambiguity.

# 3. Linear Regression Models Framework
We split into **Baseline model** and **Log linear model** (the one that will be used)

Using the OLS summary, we analyze the weight of every variable:
- Smoker (+1.554): This is the most influential variable. If a customer is a smoker, the insurance premium increases immediately by 4.73 times compared to a non-smoker with other variables constant. 
- Children (+0.102/child): Each additional child covered by the insurance policy increases the premium by 1.11 times
- Age (+0.035/year): For every one-year increase in age, the insurance cost rises by 1.04. This reflects the increasing health risk associated with aging.
- BMI (+0.013/unit): For each one-unit increase in BMI, the insurance charge increases by approximately 1.01 times. This suggests an incentive for policyholders to maintain a healthy body weight.
- Intercept (+6.96): The intercept represents a baseline value from a mathematical perspective.

# 4. Inferential Analysis
*Statistical methods used: linear regression, t-test, ANOVA*
## 4.1 Hypothesis testing
### 4.1.1 t-test
*H_0: beta for each variable is 0*

*Null hypothesis: The connection between the variables and the target doesn't exist*

**Conclusion:**
- Gender (sex_male): In most insurance datasets, the p-value for gender is often greater than 0.05. This indicates that there is no statistically significant difference in insurance charges between males and females when other factors (like BMI and smoking status) are held constant.
- Region (region_nw, region_se, region_sw): If these variables show p-values > 0.05, it implies that the geographic location of the policyholder does not significantly influence the cost of insurance relative to the reference region (Northeast). If a specific region (e.g., Southeast) has a p-value < 0.05, it suggests a statistically significant regional price difference.
- Reject the null hypothesis. There is extremely strong statistical evidence to confirm that all selected factors: age,bmi,smoker,children,sex significantly impacts insurance charges; this relationship is not due to random chance. Notably, smoking status is the most influential factor, as evidenced by its substantial coefficient (1.5538) and the highest T-score (51.319). It is followed by age, which also shows a highly significant impact with a T-score of 39.585 and a coefficient of 0.0345.
### 4.1.2 ANOVA
*H_0: mean of all regions are the same*

*Null hypothesis: Mean does not differ across regions*

**Conclusion:**
We reject the Null Hypothesis (H_0). There is strong statistical evidence to confirm that the geographical region is a significant predictor of insurance costs.

# 5. Conclusion
Overall Model Effectiveness: The Log-linear regression model effectively explains 76.8% of the variance in medical charges (R2). Additionally, the t-test and ANOVA provide statistical evidence that all variables have an effect.

The Effect of Lifestyle Behaviors (Smoking Status): Smoking is the strongest and most reliable predictor in the model, with a record-high t-statistic of 51.319. The 95% confidence interval indicates that medical costs for smokers are approximately 4.45 to 5.01 times higher than those for non-smokers. This provides compelling evidence that the health risks associated with tobacco use lead directly to a significant insurance financial burden.

Impact of Biological and Demographic Factors: Age is the strongest predictor in this group (t = 39.585), with each additional year increasing costs by 1.034 to 1.0367 times. This is followed by the number of children (t = 10.053), which raises charges by 1.085 to 1.129 times per child. BMI and Gender also show high statistical significance (P = 0.00), confirming that higher body mass and being male correlate with increased premiums. The narrow confidence intervals excluding 1 allow us to reject the null hypothesis ( Ho), proving these factors are precise and significant drivers of medical financial burden.

Impact of Geographical Regions: The results indicate that costs in the Southeast and Southwest regions are significantly lower than those in the reference region (P < 0.05). However, the Northwest region shows no statistically significant difference (P = 0.076 > 0.05), suggesting that this specific location does not have a marked impact on insurance premiums.

# 6. Recommendation
- **For Insurance Companies:** Insurance companies can use this model to set fairer prices for everyone. Instead of charging the same rate, they can offer lower costs to people with healthy habits, like non-smokers or those with a healthy BMI. To save money in the long run, companies should also create support programs to help their customers quit smoking or lose weight. This is a "win-win": customers get healthier, and the company pays less for expensive medical claims later on.
- **For Individual Customers:** For customers, the data shows that changing your lifestyle is the fastest way to save money. Quitting smoking has a much bigger impact on your wallet than moving to a new city or worrying about getting older. Also, keeping your BMI under 30 is not just good for your heart; it is a smart financial move. Maintaining a healthy weight can help you avoid high medical bills and significantly lower your yearly insurance payments.




