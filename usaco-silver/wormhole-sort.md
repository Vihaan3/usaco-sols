# Wormhole Sort

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=992" %}

### Problem-Solving

Attempt 1: I got a weird partial solution within 10 minutes of reading the problem, but I couldn't figure out anything else for the next 10 minutes that I tried to think. I then spent over 2 hours trying to understand the solution, and now I've kinda finally got it.&#x20;

Attempt 2:&#x20;

My initial thought was to adapt the [Redistributing Gifts](redistributing-gifts.md) official solution (use dfs to find what the min widths would be (instead of just whether it would reach) -> while there is a number that isn't in the right spot, move it to the right spot and adjust the global min width if the min width to get to the right spot is lower).&#x20;

The editorial solution is much more elegant and easier to implement. I think for some reason I have some subconscious prejudice against recognizing when to use binary search because I've never once used it to solve a USACO problem and often think of a gnarlier solution when an elegant one is staring me in the face. &#x20;

I honestly don't know why this problem was so hard for me in the last attempt (both at first glance and in trying to understand the editorial). It's a relatively straightforward problem with a relatively straightforward editorial.&#x20;

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <queue>
#include <fstream>

int main()
{
	std::ifstream fin ("wormsort.in");
	std::ofstream fout("wormsort.out");
	int n, m;
	fin >> n >> m;

	std::vector <int> cows(n);
	std::vector<std::vector<std::pair<int, int>>> adj (n);

	for (int i = 0; i < n; i++)
	{
		fin >> cows[i];
		cows[i]--;
	}
	
	std::vector <int> weights;
	for (int i = 0; i < m; i++)
	{
		int a, b, w;
		fin >> a >> b >> w;
		a--; b--;
		weights.push_back(w);
		adj[a].push_back(std::make_pair(b, w));
		adj[b].push_back(std::make_pair(a, w));
	}

	auto cows2 = cows;
	std::sort(cows2.begin(), cows2.end());
	if (cows == cows2)
	{
		fout << -1;
		return 0;
	}


	std::sort(weights.begin(), weights.end());
	int high = m-1;
	int low = 0;
	int mid = (low + high) / 2;
	int weight = weights[mid];
	int ans = -1;

	while (low <= high) 
	{
		mid = (low + high) / 2;
		weight = weights[mid];
		std::vector <int> connected(n+1);
		int cc_counter = 1;

		for (int i = 0; i < n; i++)
		{
			if (connected[i] == 0)
			{
				std::vector <int> memory;
				memory.push_back(i);

				while (memory.size() != 0)
				{
					int curr = memory.back();
					memory.pop_back();
					connected[curr] = cc_counter;

					for (auto a : adj[curr])
					{
						if (a.second >= weight && connected[a.first] == 0)
						{
							memory.push_back(a.first);
						}
					}
				}
			}

			cc_counter++;
		}	

		bool valid = true;

		for (int i = 0; i < n; i++)
		{
			if (cows[i] != i)
			{
				if (connected[i] != connected[cows[i]])
				{
					valid = false;
					break;
				}
			}
		}

		if (valid)
		{
			low = mid + 1;
			ans = weight;
		}
		else
		{
			high = mid - 1;
			
		}

	}
	fout << ans;
}
```
