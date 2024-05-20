# Moorbles

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1400" %}

Takeaway: Just keep going! Once you have a solution for a subtask, keep trying to optimize the heck out of it and go as far as that will take you. It seems like these problems are designed so that just iteratively optimizing an initial solution for each subtask will eventually get you to a full solution.&#x20;

<pre><code>first solution idea:
Use next_permutation or just do recursion to create all the possible combos
<strong>Sort the combos in increasing lexicographical order
</strong>For each combo:
	Loop through all the turns:
		For each turn, choose the highest number that is of the opposite type as the current in the combo


second solution idea:

Pre-identify for each turn what happens if you say even/odd (remember that you will gain if there is all of a certain kind and you choose that)
Loop thru and do the best case scenario to see if it is possible (whatever gives you least loss/highest gain)
If it is possible, loop through:
	as long as doing an even won't lead to immediate death, do an even else do an odd
	
</code></pre>

{% code overflow="wrap" %}
```
// Official Pseudo-code
Subtask 1:
Basically the same as my first solution idea + the precomputation from the second idea

Subtask 2:
Merge the checking and the generation into one recursive function]
As you're going, keep checking whether the current sequence would work if you proceeded to follow the best case scenario (without worrying about evens and odds)
If it can't work, you can immediately break out

Full solution:


```
{% endcode %}
