# Barn Tree

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1254" %}

#### Attempt 1: Failed all but the first test case

```
// Initial Pseudo-Code
dfs 
	Keep dfs-ing until you reach a node that is less than 0


vector of vector for the output called output

ship(origin, dest, amount)
	move amount from origin to dest (subtract from origin and add to dest)
	if bales[dest] > 0:
		add it to over
	push_back origin, dest, amount to output
	
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

```cpp
// Code implementing that pseudo-code
#include <iostream>
#include <vector>

std::vector <std::vector<int>> output;
std::vector <int> bales;
std::vector <std::vector<int>> adj;
std::vector <int> over;

int num = 0;
int tracker = 0;
int min = 2147483647;
std::vector<bool> visited;

void dfs(int j)
{
	if (bales[j] < 0)
	{
		tracker = j;
		return;
	}
	if (num > min || visited[j])
	{
		return;
	}
	visited[j] = true;
	for (auto u : adj[j])
	{
		num++;
		dfs(u);
	}
}

void reset_visited()
{
	for (int i = 0; i < visited.size(); i++)
	{
		visited[i] = false; 
	}
}

void ship(int origin, int dest, int amount)
{
	bales[origin] = 0;
	bales[dest] += amount;
	if (bales[dest] > 0)
	{
		over.push_back(dest);
	}
	std::vector<int> rand = { origin + 1, dest + 1, amount };
	output.push_back(rand);
}

int main()
{
	int n;
	std::cin >> n;
	bales = std::vector<int>(n);
	adj = std::vector<std::vector<int>>(n);
	visited = std::vector<bool>(n);
	int average = 0;
	for (int i = 0; i < n; i++)
	{
		std::cin >> bales[i];
		average += bales[i];
	}
	average /= n;
	for (int i = 0; i < n - 1; i++)
	{
		int a, b;
		std::cin >> a >> b;
		a--;
		b--;
		adj[a].push_back(b);
		adj[b].push_back(a);
	}
	for (int i = 0; i < n; i++)
	{
		bales[i] -= average;
		if (bales[i] > 0)
		{
			over.push_back(i);
		}
	}

	for (int k = 0; k < over.size(); k++)
	{
		int i = over[k];
		if (adj[i].size() == 1)
		{
			ship(i, adj[i][0], bales[i]);
			continue;
		}
		int track = 0;
		for (int j = 0; j < adj[i].size(); j++)
		{
			int l = adj[i][j];
			dfs(l);
			if (num < min)
			{
				min = num;
				track = tracker;
			}
			num = 0;
			tracker = 0;
			reset_visited();
		}
		ship(i, track, bales[i]);
	}

	std::cout << output.size() << std::endl;
	for (auto out : output)
	{
		std::cout << out[0] << " " << out[1] << " " << out[2] << std::endl;
	}

}
```

**Attempt 2: Re-implementing the official pseudo-code**

```
Overview
Take in input, make adjacency list, process by average
Recursively for each node in the tree find the sum of the subtree from that node
Recurse down the tree. Move values from all positive nodes in the subtree to the root node
Recurse down the tree. Move values from the root to all negative values
```
