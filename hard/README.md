# Hard Test

## Step 1

-   implementing cost function into the cost_general_functions.c in changepoint package on CRAN [<https://github.com/rkillick/changepoint/blob/main/src/cost_general_functions.c>]

``` c
#include <float.h> // For DBL_MIN to avoid log(0)

double mll_binary(double x, double x2, double x3, int n, double shape) {
    if(n == 0) return 0;
    
    double p_hat = x / n; 
    if(p_hat <= 0) p_hat = DBL_MIN;
    if(p_hat >= 1) p_hat = 1 - DBL_MIN;

    // Calculate the negative log-likelihood
    double cost = -(x * log(p_hat) + (n - x) * log(1 - p_hat));
    return cost;
}
```

## Step 2

-   modify PELT_one_func_minseglen.c so that binary cost function will be used for the PELT implementation [<https://github.com/rkillick/changepoint/blob/main/src/PELT_one_func_minseglen.c>]

-   Add Function to the Decision Structure

``` c
else if (strcmp(*cost_func,"binary")==0){
  costfunction = &mll_binary;
}
```
