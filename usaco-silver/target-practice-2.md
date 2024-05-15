# Target Practice 2

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1398" %}

Subtask 2

```
Summarizing, the slope we should have on each vertex of a target is:

Upper Right: negative
Lower Right: positive
Leftmost vertices: Sort these from smallest to largest based on y-value, and assign the lowest points negative slopes and the rest positive slopes

Go through the positive slopes from greatest to least. For each slope, target the point that results in the highest corresponding y-intercept out of all the points that have not been targeted so far. 


Go through the negative slopes from least to greatest. For each slope, target the point that results in the lowest corresponding y-intercept out of all the points that have not been targeted so far. 
```
