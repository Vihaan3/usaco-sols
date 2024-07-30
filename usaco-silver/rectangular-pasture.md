# Rectangular Pasture

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1063" %}

Here, I got faked out by the sample test case. I spent \~30 minutes during a practice contest trying to dream up ways to figure out which pairs didn't work that I forgot that even 2^100 was far beyond what even a long long could hold.&#x20;

You get to the real solution by iterating over all pairs of upper and lower bounds and using 2d prefix sums to find how many points could be right/left bounds. &#x20;
