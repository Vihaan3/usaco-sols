# Triangles

{% embed url="http://www.usaco.org/index.php?page=viewproblem2&cpid=1015" %}

This was a hard problem. I think a valuable lesson I learned here was to spend way more time playing with hand-made test cases on the whiteboard, and to spend more time on the whiteboard in general. Every mini-logical-breakthrough that I needed to get to the full solution could've happened if I'd just spent more time figuring it out on the whiteboard instead of staring at a screen and thinking.&#x20;

Pseudocode for the final solution:&#x20;

```
A struct fence that stores x, y, sum for bases, sum for heights
A vector fence of type fences
A vector for x-coords that's double the max input size and tracks (emphasis) y coordinates and indices
A vector for y-coords that's double the max input size and tracks (emphasis) x coordinates and indices
X-coords and y-coords will basically track y-coords for all positions along a specific x-coord/x-coords for all positions along a specifc y-coord

Take input into fences. Update xcoords and ycoords appropriately 
for all positions in x-coords:
    sort all positions along this x-coord
    find the heightsum for the first position naively
    loop through all the rest and find their heightsums using the recurrence relation
Ditto for y-coords but with basesum
Output the sum of (base_sum*height_sum) for each post + all the modification logic
```
