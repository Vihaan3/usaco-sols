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

<pre><code><strong>// Elaborated psuedo-code
</strong><strong>std::vector&#x3C;std::pair&#x3C;int, int>> steps; -> keeps track of all movements
</strong>
pour (pourer, pouree, int num1, num2)
{
	steps.push_back(std::make_pair(num1, num2));
	if (pourer[pourer.size()-1] == pouree[pourer.size()-1])
		delete the last element of pourer
	else
		pouree.push_back(pourer[pourer.size() - 1]);
		delete the last element of pourer
	
}


solve(tube1, tube2, int p)
{
	tube3 = "";
	// Compress runs
	temp1 = ""
	temp2 = ""
	loop through tube1:
		if current character != previous character
			add to temp1
	loop through tube2:
		if current character != previous character
			add to temp2
	tube1 = temp1;
	tube2 = temp2;
	if (the last characters of tube1 and tube2 are equal)
	{
		if (tube1 has length > 1)
		{
			pour into tube 2
		}
		else
		{
			pour into tube 1
		}
	}
	if (both tube1 and tube2 have length 1)
	{
		std::cout &#x3C;&#x3C; steps.size() &#x3C;&#x3C; std::endl;
		if (p != 1)
		{
			print the steps
		}
		end;
	}
	else
	{
		if (tube1 has length > 1)
		{
			pour tube 1 into tube 3
		}
		else if (tube2 has lenght > 1)
		{
			pour tube 2 into tube 3
		}
	}
	if (tube1[0] != tube3[0])
	{
		while (tube1.size() > 1)
		{
			pour into the tube where the top character matches that of tube1
		}
		
		while (tube2.size() > 1)
		{
			pour into the tube where the top character matches that of tube2
		}
	}
	else if (tube2[0] != tube3[0])
	{
		ditto 
	}
	
	if (tube1 == tube3)
	{
		pour tube3 into tube1
	}
	
	else
	{
		pour tube3 into tube2
	}
		
}

solver()
{
	take in n and p
	take in input for the tubes as strings
	solve (tube1, tube2, p)
}


std::cin >> T
while (T--)

</code></pre>
