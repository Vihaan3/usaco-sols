# Winning Gene

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1424" %}

{% code overflow="wrap" %}
```
// Official Pseudo-code
Subtask 1.5 sol
Vector where the indices represent # of winning genes and the values represent the numbers of K, L pairings that have that # of winning genes
2d vector of sets of ints with the indices representing K, L combos 
Iterate over all positions:
	Iterate over all possible L (from 1 to the minimum of the positions distance from the beginning and the position's distance from the end):
		Loop through the string and locate the maximum position less than the og position that has a lexicographically smaller or equal substring with L and the first position after the og position that has a lexicographically smaller substring with L (stop at end of the array - L if there isn't any)
		K can be all the values between 1 and the difference of the two positions. Update all of those values

Iterate through the 2d vector and in the 1d vector increment the index of the size of each set

Subtask 2.5:
Optimize the above by using prefix sums on updating K and naively pre-computing the longest common prefix for all pairs of positions (to make comparison O(1)). 

Full Solution:
Compute lcp backwards using: lcp[i][j] = (S[i] == S[j]) + lcp[i+1][j+1] because if we know lcp[i+1][j+1], we can compute lcp[i][j] based on whether or not character i == character j  
```
{% endcode %}
