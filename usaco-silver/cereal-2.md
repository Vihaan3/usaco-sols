# Cereal 2

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1184" %}

This was yet another problem that stumped me during a practice contest. I had an intuition that the solution had something to do with graphs but I couldn't quite figure it out.&#x20;

The major unlocks are:

* Realizing that you can represent the problem well through a graph with directed edges from favorite cows to second-favorite cows where the each edge is a cow.&#x20;
* Break the problem down into connected components and dfs within each to find the order.&#x20;
  * Find and then process cycles separately.&#x20;
