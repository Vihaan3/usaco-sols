# Cowmpetency

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1374" %}

My original solution was actually pretty on-target for this one, and just missed by a bit. I got stumped by making sure that changes made to make one constraint true wouldn't disrupt another pair, but I didn't even think about the fact that I could just use a prefix-sum-like idea to store the `hi`s for every i.&#x20;

{% code overflow="wrap" %}
```
My Pseudo-Code

take in input
make a copy of the original c array, make all changeable values 1
sort the Q pairs by a
for each Q pair:
	find the max value in the section from 1 to a: P
	check all the numbers between a and b for a number that's greater than the max
			work back from a to the beginning of the section, and change the first one that's changeable to be equal to the one that's greater than the max
		if there is
				set b equal to 1+ that
			if there are no changeable ones:
				-1
		else
			make b equal to 1+ the max
		

final pass where you try to lower all the numbers if possible, check to see that everything is correct (including that upper_bound C constraint)

```
{% endcode %}

{% code overflow="wrap" %}
```
Pseudo-Code inspired by the official solution
// WATCH OUT FOR 1-INDEXING!!!

Take in the first two pieces of input (N,Q,C + c array)
Store 1 at every position that isn't already set in c, and store the ones that were originally set in a vector of bools
Create a vector, B, where B[i] = the index of the first value that is greater than the maximum of the values from up to index i. Take in input for the Q pairs in there.
Loop thru all elements:
    Loop thru all elements between this element and its B[element]:
        if the B[curr] != 0 and b[element] != b[curr]:
            std::cout << -1;
            break;
        else
            B[curr] = B[element]
Loop thru all elements (skip over the ones with B[element] == 0):
    if there is a value that is greater than max_up_to_element between element and B[element]
        if B[element] is pre-set
            std::cout << -1;
            break;
        work backwards from element:
            if B[curr_element] != 0 and B[element] < B[curr]
                std::cout << -1;
                break;
            if curr has already been set
                continue;
            else
                curr = the value in between element and B[element]
                break
    B[element] = the value in between + 1
    
check that each element is at most C
print all the elements in c
```
{% endcode %}

This pseudo-code is robust enough that I'll skip the implementation.
