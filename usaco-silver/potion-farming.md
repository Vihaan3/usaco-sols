# Potion Farming

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1375" %}

### First solution:

```
Take in tree input 
BFS on the tree 
This BFS needs to return a vector of vectors with the traversals you need. 
Vector of vectors of size n: potion_vec 
Vector of vectors of size (min_traversals): traversal_vec2 
For each traversal: 
    For each element in each traversal: 
         in potion_vec, push_back the index of the traversal it's in in traversal_vec,       
         push_back the index of the element     
for (potion in potions) 
    if it has traversals: choose the traversal that has it that has the least other potions potions++; 
    else choose the traversal that has the least potions for the traversal chosen, go thru traversal_vec and delete it from everything in potion_vec
```

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

The solution to the first subtask is to just greedily pair each leaf with it's closest potion-spawning ancestor.&#x20;

```
// O (N^2) Solution
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

```
// O (N) Solution
C(i) = number of leaves that node i is an ancestor of.
P(i) = number of potions collected by all the paths that go through i.
Pot[i] = number of potions that spawn at node i

Recursively build the solution from the leaves up to the root, using the backwards part of DFS
The value of P(i) is the sum of the values of P(c) for all children of i.
If [sum of P(c)] < C(i) for the current node i, that means that there are some unpaired leaves. Any potions found at node i are the closest potions, so we can pair them. 
If [sum of P(c)] = C(i) for the current node i, that means that all leaves have been paired with another leaf. 
```
