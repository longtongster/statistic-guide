# statistic-guide
Repo used to provide an overview of statistical tests

#### ToDO
- confounding - what is it

## type of tests

### normality 
test if data is normally distributed

`result = stats.anderson(data)`

the statistic is in `result.statistic` the critical values are in `result.critical_values`. By default these relate to [15%, 10%, 5%, 2.5%, 1.0%]. If the statisc is larger than a critical value the null hypothesis is rejected with that confidence level.

- mean - follow t-distributioin
