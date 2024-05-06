# Potion Farming

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1375" %}

### First solution:

Take in tree input BFS on the tree This dfs needs to return a vector of vectors with the traversals you need. Vector of vectors of size n: potion\_vec Vector of vectors of size (min\_traversals): traversal\_vec2 For each traversal: For each element in each traversal: in potion\_vec, push\_back the index of the traversal it's in in traversal\_vec, push\_back the index of the element for (potion in potions) if it has traversals: choose the traversal that has it that has the least other potions potions++; else choose the traversal that has the least potions for the traversal chosen, go thru traversal\_vec and delete it from everything in potion\_vec

BFS Implementation

```
// Adjacency list representation of tree

std::vector<std::vector<int>> traversals;
int index = 0;
queue <int> q;
bool visited[N];
int distance [N];
visited[x] = true;
distance[x] = 0;
q.push(x);
while (!q.empty())
{
	int s = q.front();
	q.pop();
	traversals[index].push_back(s);
	for (auto u : adj[s])
	{
		if (visited[u]) continue;
		visited[u] = true;
		distance[u] = distance[s] +1;
		q.push(u);
	}
	index++;
}
```

### Real Solution

So it turns out that I'm insanely stupid.&#x20;

Since it's a tree, of course you can just figure out the number of traversals through the number of leaves.&#x20;

```
O (n^2 solution)
Take in input as a vector of potions and an adjacency list of rooms
Create a vector that indexes on the room numbers the potions will appear in: appear
Create a vector that keeps track of parent nodes
Loop through the tree and calculate the number of leaves
Loop through the number of traversals:
	Increment appear[potions[number]]
Run a dfs that keeps track of the parent nodes and skips returns 
Loop through all leaf nodes:
	Backtrack the current traversal and add 1 to the count if you find a room where there is a potion

```
