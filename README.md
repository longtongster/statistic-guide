# Guide on statistics

Repo used to provide an overview of statistical tests.

#### ToDo
- confounding - what is it
- conditions that hold for certain tests
- autocorrelation
- maybe add at a later stage how many observations we should have for each test or group
- rearrange the items below in logical order

### Effects
A measure of strenght between two variables. The `p_value` measures if there is a relation, the effect size is the strenght of the relationship.

One measure to calculate `Cohen's d`. 

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

# Hypothesis Testing

**The power of a test**:
_if the alternative hypothesis (Ha) is true, how likely is our test to reject the null hypothesis (H0) givn the data we have suplied it?_

in the scipy stats module there are several ways to calculate the power of a test, e.g. `stats.power.TTestIndPower(effect_size=0.2, nobs1=100, alpha=0.05)`.

you can also solve the number of observations to meet a certain power

`nobs1 = TTestIndPower().solve_power(effect_size=0.2, nobs1=None, alpha=0.05, power=0.8)`

## Parametric tests

For these test the underlying data has to be normally distributed. 
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

