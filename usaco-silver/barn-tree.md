# Barn Tree

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1254" %}

```
dfs 
	Keep dfs-ing until you reach a node that is less than 0


vector of vector for the output called output

ship(origin, dest, amount)
	move amount from origin to dest (subtract from origin and add to dest)
	if bales[dest] > 0:
		add it to over
	push_back origin, dest, amount to output
	

Fleshed out
Pre-processing:
	Input:
		Take in # of bales input as a vector: bales
		Take in roads input as an adjacency list (vector of vectors of size N by N where you push back the connection into both): adj
		Calculate the average
	Create a vector over for the barns with too much bale
	Loop through all the values in bales:
		Subtract each position by the average
		If the value is > 0:
			add it to over
Loop through over:
	If the barn only has one connection:
		ship (og_barn, adj[og_barn][0], bales[og_barn]);
		break;
	int min = 0;
	int track = 0;
	Loop through all the connections in adj:
		dfs(connection) + keep track of all the times it runs
		update min and track based on the minimum
	ship(og_barn, track, bales[og_barn])
	
Print output
```
