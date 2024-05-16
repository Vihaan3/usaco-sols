# Test Tubes

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1399" %}

```
// First Attempt Psuedo-code
while (true)
	if the first two test tubes only have one layer
		end
	else
		if the first and third test tubes only have one layer
			move the third to the second
			end
		if the second and third 
			move the third to the first
			end
	check all 3 tubes to see if any 2 are the same at top
		if so, 
			combine on the one that has fewest other layers underneath it
			otherwise, combine on the one most likely to 
		else, move the bigger stack at the top to the empty test tube
			if neither is the bigger stack
				move randomly

while you're doing this, continuously keep track of the number of layers of each tube 
```

```
// Official Solution Pseudo-code
Compress runs of the same number at each step

1. If the last characters of f and s are equal, choose any tube with a string of length greater than one and pour it into the other tube.
2. If both f and s now have length one, we're done. Otherwise, we're in a case where the beaker must be used. Choose any tube with a string of length greater than one and pour it into the beaker. The last characters of both tube strings are now equal.
3. Suppose the beaker now contains liquid i. Choose the tube whose string has first character not equal to i, and repeatedly pour from it until its string has length equal to one. We should pour it into either the beaker or the other tube depending on which pour reduces the number of characters after compressing by one.
4. Next, pour from the other tube until its string has length one.
5. Finally, pour from the beaker into one of the tubes.
```
