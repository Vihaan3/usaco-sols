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
