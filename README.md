# catfit

This is an attempt to build a classification model based on curve/surface parametrization.
Assume we have a set of features `X` and its corresponding labels `y`(with `k` distinct labels).
The idea is to assign an axis in `R^k` to each of the labels and find a curve/surface which transforms `X` into `R^k`,
such that the coordinate with maximum absolute value of each point corresponds with the axis assigned to the label of that point.

For example if a point in X is labelled as "A" and we have assign this label to the "Z" axis, the point could possibly get mapped to (2,-3,4), where the value of the "Z" coordinate is higher.


The parametrization for a single feature `t` is defined like this:

` g(t) = (a_0 + b_0t + c_0t^2 ..., a_1 + b_1t + c_1t^2 ..., a_2 + b_2t + c_2t^2 ...)`

The cost function is defined like this:
```
p_0, p_1, ... p_k = g(t)
J(p) = max(|p_0|,|p_1|, ...|p_k|) - |correct_coord(p_0, p_1, ... p_k)|
```

Identified problems with the current implementation:
- The total sum of the absolute values of the weights (coefficients of the curve) tends to grow with each iteration of the gradient descent.
- The polynomial curve is not flexible enough to adapt to multiple classes. Other curves should be considered.
- The initialization of the weights is done randomly within the interval `0.1*(-0.5, 0.5)`. Better approach could be considered.
 
