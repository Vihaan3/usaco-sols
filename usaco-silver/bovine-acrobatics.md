# Bovine Acrobatics



{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1350" %}

### Problem-Solving

I got an O(n^2) solution pretty early on that passed 9/15 test cases, but I just couldn't figure out a more optimized solution.  The official solution is elegant, and I think I would've been able to get it if I'd focused more on looking at the order of the subtasks. I try to get the best solution I can right away, and that worked in bronze, but I think it's why I'm struggling a little bit with silver.

### Implementation

Pseudo-code and implementation for 50% solution&#x20;

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

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main ()
{
	int n, m, k;
	std::cin >> n >> m >> k;

	std::vector <std::pair <int, int>> vec (n);
	for (int i = 0; i < n; i++)
	{
		std::cin >> vec[i].first >> vec[i].second;
	}
	std::sort(vec.begin(), vec.end(), std::greater<std::pair<int, int>>());
	std::vector <std::vector <int>> towers;
	towers.push_back(std::vector <int> {vec[0].first});
	vec[0].second--;
	int num = 0;
	for (auto &v : vec)
	{
		while (v.second > 0)
		{
			bool enter = false;
			if (towers[0][towers[0].size() - 1] - v.first >= k)
			{
				enter = true;
				towers[0].push_back(v.first);
				towers.push_back(towers[0]);
				towers.erase(towers.begin());
				v.second--;
				num++;
			}
			else
			{
				if (towers.size() < m)
				{
					enter = true;
					towers.push_back(std::vector<int> {v.first});
					v.second--;
					num++;
				}
			}
			if (!enter)
				break;
		}	
	}

	std::cout << num + 1;
}
```

Full Solution

```python
from collections import deque
N, M, K = map(int, input().split())
 
pairs = []
for _ in range(N):
	w, a = map(int, input().split())
	pairs.append([w, a])
pairs.sort(reverse = True)
 
towers = deque()
towers.append([1e100, M])
answer = 0
for w, a in pairs:
	remaining = a
	while len(towers) > 0 and remaining > 0 and w + K <= towers[0][0]:
		if towers[0][1] > remaining:
			towers[0][1] -= remaining
			remaining = 0
		else:
			remaining -= towers[0][1]
			towers.popleft()
	cnt = a - remaining
	if cnt > 0:
		towers.append([w, cnt])
		answer += cnt
	
 
print(answer)

```
