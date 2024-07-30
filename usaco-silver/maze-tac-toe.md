# Maze Tac Toe

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1134" %}

I tried to solve this problem during a practice contest and miserably failed.&#x20;

There were two hidden unlocks for this problem that I figured out after reading the solution.

* You want to evaluate the dfs based on board state and not maze state.
* You can track maze and board states together in one big array by thinking about board states as numbers (and using some fancy base-3 stuff). &#x20;
