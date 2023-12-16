# statistic-guide
Repo used to provide an overview of statistical tests

#### ToDo
- confounding - what is it
- conditions that hold for certain tests
- autocorrelation

## type of tests

### test for normality 
The Anderson-Darling test can be used to determine if you data is distributed normal.

`result = stats.anderson(data)`

the statistic is in `result.statistic` the critical values are in `result.critical_values`. By default these relate to [15%, 10%, 5%, 2.5%, 1.0%]. 

`result.significance_level[result.statistic > result.critical_values]`

If the statisc is larger than a critical value the null hypothesis is rejected with that confidence level.

### Normal distribution in SciPy

If your data is normal (e.g after using the anderson test) you can fit the mean and standard deviation using:


`mu, std = stats.norm.fit(data)`

use the .cdf method to get the cumulative distibution function

`prob = stats.norm.cdf(70000, loc=mu, scale=std)`

### Pearson's R in SciPy

Pearson's measure linear correlation.One can calculate pearson's R in SciPy using:

`r, p_value = stats.pearsonsr(data1, data2)`

If the `p_value` the null hypothese is that the series are uncorrelated. 

squaring pearson's R gives the percent variation in one sample in the other.




- mean - follow t-distributioin
