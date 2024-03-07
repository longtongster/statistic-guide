# Guide on statistics

The objective of this repo is to have a summary on basic statistics and statistical test. 

references:
- https://real-statistics.com/students-t-distribution/two-independent-samples-t-test/two-sample-t-test-advanced/

#### ToDo
- stats.zscore for outliers check
- idea is to create a separate page that contains derivations for most test statistics (e.g. how do we get the that the mean of a sample with unknown variance is t distributed) 
- derive the results of difference in means (see inferential statistics) with the pooled and non pooled versions independent samples of two groups (add this (see above))
- conditions that hold for certain tests
- autocorrelation
- maybe add at a later stage how many observations we should have for each test or group
- rearrange the items below in logical order


## Genereric topics

### Types of Missing Data

- Missing completely at random (MCAR). When data are MCAR, the fact that the data are missing is independent of the observed and unobserved data.15 In other words, no systematic differences exist between participants with missing data and those with complete data
- Missing at random (MAR). When data are MAR, the fact that the data are missing is systematically related to the observed but not the unobserved data.15 For example, a registry examining depression may encounter data that are MAR if male participants are less likely to complete a survey about depression severity than female participants. That is, if probability of completion of the survey is related to their sex (which is fully observed) but not the severity of their depression, then the data may be regarded as MAR
- Missing not at random (MNAR). When data are MNAR, the fact that the data are missing is systematically related to the unobserved data, that is, the missingness is related to events or factors which are not measured by the researcher. 

### Experiments

#### Definitions:
- Treatment: explanatory/independent variables
- Response: response/dependent variable

#### Controlled experiments:
- participants are assinged by researchers to either treatment group or control group
  - treatment group sees advertisements
  - control group does not
- Groups should be comparable, so that causation can be inferred
- If groups are not comparable this could lead to confounding (bias)
  - Treatment group average age (e.g. 25)
  - Control group average age (e.g. 50
  - age is a potential confounder

#### The golden standard of experiments:
- Randomized controlled trial
  - Particiants are assigned to treatment/control ranomly, not based on any other characteristics.
  -  Choosing randomly helps ensure that groups are comparable
- Placebo
  - Resembles treatment, but has not effect
  - Participants will not know which group they're in.
  - In clinical trials, a sugar pill ensures that the effect of the drug is actually due to the drug itself and not the idea of receiving the drug. 
- Double-blind trial
  - Person administring the treatment/running the study doesn't know whether the treamt metn is real of placebo.
  - Prevents bias in the response and/or analysis of results. 

#### Observational studies
- Participants are not assigned randomly to groups
  - Participants assing themselves, usually based on pre-existing characteristics.
- Many research questions are not conducive to a controlled experiment
  - e.g. you cannot force someone to smoke
- Establish association, not causation
  - Effects can be confounded by factors that got certain people into the control or treatment group
  - There are ways to control for confounders to get more reliable conclusions about association.

### Confounding

- In causal inference, a confounder (also confounding variable, confounding factor, extraneous determinant or lurking variable) is a variable that influences both the dependent variable and independent variable, causing a spurious association.

### Statistical Validity
Statistical validity can be defined as the extent to which drawn conclusions of a research study can be considered accurate and reliable from a statistical test. To achieve statistical validity, it is essential for researchers to have sufficient data and also choose the right statistical approach to analyze that data.

- Construct Validity: it ensures that the actual experimentation and data collection conforms to the theory that is being studied.
- Content Validity: this validity ensures that the test or questionnaire that is prepared completely covers all aspects of the variable being studied.
- Face Validity: this type of validity estimates whether the given experiment actually mimics the claims that are being verified.
- Conclusion Validity: this validity ensures that the conclusion is achieved from the data sets obtained from the experiment are actually correct and justified without any violations.
- Internal Validity: it is a measure of the relationship between cause and effect being studied in the experiment.
- External Validity: this validity is a measure of how to apply the results from a particular experiment to more general populations. Furthermore, it informs the analyst whether or not to generalize the results of a particular experiment to all other populations or to some populations with particular characteristics.

### Sampling techniques:
1. Simple random sampling - each case of the population has the same probability of being selected.
2. Systematic sampling - Randomly select the first case then select every k-th case.
3. Stratified sampling - guarantees that the sample will be representative on the selected (stratifiying) variables. (e.g. group population by nationality and then sample the same fraction for each nationality)
4. Cluster sampling - take the sample from a cluster (e.g. a US state) and use that sample from the state to infer results on the total US populations.

### Sampling distribution:
A sampling distribution is the probabilistic distribution of a statistic for all possible samples of a given size (N). Every application of inferential statistics involves three distributions: population, sampling and sample.

### Effects
A measure of strenght between two variables. The `p_value` measures if there is a relation, the effect size is the strenght of the relationship.

One measure to calculate `Cohen's d`. This measure seems similar or the same to the t-test value used to test if differences in mean between two samples is the same. 

Effect size of pearson's correlation r is $r^2$.

Effect size for categorical variables:
- Chi-square statistic from contingency table
- n = total numbers
- d = degrees of freedom = min(rows-1, cols-1)

$$ \text{Cramer's V} = \sqrt{\frac{chi^2/n}{d}}$$

This always returns a value between 0 and 1. With 0 meaning no relationshipt and 1 meaning a perfect relationship. 

Using python we can use 

`chi2, p, d, e = stats.chi2_contingency(contingency_table)`

use this `chi_2` in the above formula.

### Relation between distributions

If $Z$ is standard normal then $T=Z^2$ is a chi-square

## t-distribution 

Let $Z$ and $V$ be independent random variables following a standard normal distribution and a chi-squared distribution with $\nu$ degrees of freedom, respectively
\begin{split}
Z &\sim \mathcal{N}(0,1) \\
V &\sim \chi^{2}(\nu) \; .
\end{split}

An F-distribute random variable is defined as the ration of two `chi-squared` random variables, divided by their degrees of freedom. 

$$X \sim \chi^2(u), \; Y \sim \chi^2(v) \quad \Rightarrow \quad F = \frac{X/u}{Y/v} \sim \mathrm{F}(u,v)$$

where $X$ and $Y$ are independent of each other 


# Hypothesis Testing

**The power of a test**:
_if the alternative hypothesis (Ha) is true, how likely is our test to reject the null hypothesis (H0) givn the data we have suplied it?_

in the scipy stats module there are several ways to calculate the power of a test, e.g. 

`stats.power.TTestIndPower(effect_size=0.2, nobs1=100, alpha=0.05)`.

you can also solve the number of observations to meet a certain power

`nobs1 = TTestIndPower().solve_power(effect_size=0.2, nobs1=None, alpha=0.05, power=0.8)`

one can set the `effect_size` to the outcome Cohen's d test.

## Parametric tests

parametrric tests generally require assumptions about the shape and parameters of the distibution. (e.g. test the underlying data has to be normally distributed.)
 
- z-test
  - can be used to test a statistic on proportions or different
  - can be used to test if proportions of two groups are the same
  - can be used to test proportions of two groups with paired data. 
  - can be used to test mean of a population given the standard deviation is known
- t-test
- f-test
- Independent sample t-test
- ANOVA
- Paired sample t-test
- Pearson's R

### Test two-sample t-test

The two-sample t-test can be used to test if the mean of two groups is statistically different. 

The null hypothesis is that the means are the same. There are several different alternatives to test such as one-sided (mean of group one is higher or lower than of group two) or two-sided test.

a one-sided test can be performed with scipy

`t_test = stats.ttest_ind(group1, group2, alternative='less')`

`t_test.p_value < 0.05` 

### Paired t-test

Here it is key that data is paired. So we have observations from the same respondents for example different years (e.g election outcomes in 2012 and 2016 of the same state). The test is used to test for differences in mean for paired data. Here the data is not independendent (e.g. election outcomes of the same state in different years.) Here you calculate the difference for each obervations and than take the mean of the differences

$$ t = \frac{chi^2/n}{d} $$ 
with degrees of freedom $df=n_{diff} -1$

below the H0 is that the difference is zero y=0.

```import pingouin
pingouin.ttest(x=sample_data['diff'], y=0, alternative="less")
```

alternatively one use pandas series directly

```import pingouin
pingouin.ttest(x=sample_data['colA'], y=sample_data['colB'], paired=True, alternative="less")
```


### test for normality 
The Anderson-Darling test can be used to determine if you data is distributed normal.

`result = stats.anderson(data)`

the statistic is in `result.statistic` the critical values are in `result.critical_values`. By default these relate to [15%, 10%, 5%, 2.5%, 1.0%]. 

`result.significance_level[result.statistic > result.critical_values]`

If the statisc is larger than a critical value the null hypothesis is rejected with that confidence level.

### Pearson's R in SciPy

Pearson's measure linear correlation.One can calculate pearson's R in SciPy using:

`r, p_value = stats.pearsonsr(data1, data2)`

If the `p_value` the null hypothese is that the series are uncorrelated. 

squaring pearson's R gives the percent variation in one sample in the other.

### ANOVA

The null hypothesis under an ANVOA test is that the mean in several groups is the same. The alternative hypothesis is that at least one mean is different. There are several assumptions:
- responses for each factor (group) are normally distributed.
- responses for each factor have the same variance. (Levene test - see below)

the one way anova 

`s, p_value = stats.f_oneway(data1, data2, data3)`

If the p_value is lower than the confidence level we reject the null huypotheses.

### Levene test

This test if variance in groups (factors) are the same. This test is on two groups not more. The null hypotheses is that the variances are the same.  

`s, p_value = stats.levene(data1, data2)`

If the p_value is lower than the confidence level we reject the null huypotheses.

## Non-parametric test

- These do not require the data to be normal
- are sometimes less powerfull.
- useful for ranked order

Examples:
- Wilcoxon-Man-Whithney U test
- Krusal-Wallis test
- Mood's median test
- Kendall's tau

### Mood's median test

Compares medians from two paired measurement. The paired measurments can be seen as two different features in a matrix

`s, p_value, m, table = stats.median_test(data1, data2)`

### Kendall's tau

Works with ranking data which is not normally distributed. takes values between -1 and 1.  

`tau, p_value = stats.kendalltau(data1, data2)`


## Distributions

### Normal distribution in SciPy

If your data is normal (e.g after using the anderson test) you can fit the mean and standard deviation using:


`mu, std = stats.norm.fit(data)`

use the .cdf method to get the cumulative distibution function

`prob = stats.norm.cdf(70000, loc=mu, scale=std)`
