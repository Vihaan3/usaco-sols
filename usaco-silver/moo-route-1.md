# Moo Route

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1304" %}

```cpp
#include <vector>
#include <iostream>
#include <limits.h>
#include <algorithm>

int main()
{
	int n, m;
	std::cin >> n >> m;
	std::vector<std::vector<std::pair<int, std::pair<int, int>>>> flights(n);
	std::vector <int> layoffs(n);
	std::vector<int> time(n);
	for (int i = 0; i < m; i++)
	{
		int a;
		std::cin >> a;
		a--;
		std::pair<int, std::pair<int, int>> temp;
		std::cin >> temp.first >> temp.second.first >> temp.second.second;
		temp.second.first--;
		flights[a].push_back(temp);
	}

	for (int i = 0; i < n; i++)
	{
		std::cin >> layoffs[i];
	}

	for (int i = 1; i < n; i++)
	{
		time[i] = INT_MAX;
	}

	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < flights[i].size(); j++)
		{
			flights[i][j].first -= layoffs[i];
		}
		std::sort(flights[i].begin(), flights[i].end(), std::greater<std::pair<int, std::pair<int, int>>>());
	}

	std::vector <std::pair<int, int>> queue;
	queue.push_back(std::make_pair(0, 0));
	int iterator = 0;

	while (iterator < queue.size())
	{
		int pos = queue[iterator].first;
		int curr_time = queue[iterator].second;
		int orig_time = time[pos];
		time[pos] = std::min(time[pos], curr_time);

		if (orig_time != time[pos] || iterator == 0)
		{
			for (int i = 0; i < flights[pos].size(); i++)
			{
				int check = flights[pos][i].first;
				if (iterator == 0)
				{
					check += layoffs[0];
				}
				if (curr_time <= check)
				{
					queue.push_back(flights[pos][i].second);
				}
				else
					break;
			}
		}
		iterator++;
	}

	for (auto t : time)
	{
		if (t == INT_MAX)
		{
			t = -1;
		}
		std::cout << t << std::endl;
	}
}
```
