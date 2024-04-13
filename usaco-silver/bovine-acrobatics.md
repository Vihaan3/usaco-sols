# Bovine Acrobatics



{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1350" %}

### Problem-Solving

I got an O(n^2) solution pretty early on that passed 9/15 test cases, but I just couldn't figure out a more optimized solution.  The official solution is elegant, and I think I would've been able to get it if I'd focused more on looking at the order of the subtasks. I try to get the best solution I can right away, and that worked in bronze, but I think it's why I'm struggling a little bit with silver.

My new problem-solving strategy will be:

1. Read through the problem, **look at the time complexity,**
2. Ignoring the time complexity for now, try to observe some patterns while solving the sample test cases&#x20;
3. Think of the most simple solution possible ignoring the time complexity and plan it out completely
4. If that solution unoptimal, bookmark it and then try to see if you can optimize it in any way AND/OR look at the subtasks and see what they might provide insight into more optimized solutions
5. Once you have a solution, test it yourself with a few hand-generated test cases
6. Write a description of the solution down
7. Write out detailed pseudo-code that is just advanced enough that it wouldn't take any brain power to implement (you've already done all the thinking)
8. Flesh that out into code

### Implementation

Pseudo-code

```
if the current cow can be on any tower, it can go on the tower with the heaviest cow on top
if you sort the cows and the towers (both by decreasing weight), then what you can do is, on each step, see if you can put the current cow on the first tower (if it is light enough that the difference is greater than or equal to K). if it can, putit on the tower and put that tower at the end. else turn that cow into a tower and put it at the end

take in initial input
take in input into a vector of pairs
sort the vec of pairs by decreasing (not the standard sorting algo) 
create a vector of vectors for the towers
insert the top cow from the vec of pairs and -- the number of cows that now have that weight
int num = 0;
for each pair in the vec of pairs
	while the number of cows in this pair hasnt run out
		if the difference between the last cow in the first index of the towers and the weight of this cow is greater than or equal to K
			push_back into that index 
			put that tower at the end
			num++;
		else
			if the size of the vec of vecs is less than M
				push_back this cow as a vector into the vec of vecs
				num++

std::cout << num;

```
