# Triangles

{% embed url="http://www.usaco.org/index.php?page=viewproblem2&cpid=1015" %}

This was a hard problem.&#x20;

Pseudocode for the final solution:&#x20;

```
A struct fence that stores x, y, sum for bases, sum for heights
A vector fence of type fences
A vector for x-coords that's double the max input size and tracks x coordinates and indices
A vector for y-coords that's double the max input size and tracks y coordinates and indices

Take input into fences and then put into x-coords and y-coords 
for all positions in x-coords:
    
Ditto for y-coords
Output the sum of (base_sum*height_sum) for each post + all the modification logic
```
