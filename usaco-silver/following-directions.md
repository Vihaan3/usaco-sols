# Following Directions

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1279" %}

```cpp
#include <vector>
#include <iostream>

int calc(std::vector<std::vector<int>> costs, std::vector<std::vector<int>> tracker)
{
	int sum = 0;
	for (int j = 0; j < costs.size()-1; j++)
	{
		sum += tracker[costs.size() - 1][j] * costs[costs.size() - 1][j];
		sum += tracker[j][costs.size() - 1] * costs[j][costs.size() - 1];
	}
	return sum;
}

std::vector<std::vector<int>> adder (std::vector<std::vector<char>> directions, std::vector<std::vector<int>> tracker, int amount, int i, int j)
{
	while (i < directions.size() && j < directions.size())
	{
		if (directions[i][j] == 'R')
		{
			j++;
			tracker[i][j] += amount;
		}
		else
		{
			i++;
			tracker[i][j] += amount;
		}
	}
	return tracker;
}


int main()
{
	int n;
	std::cin >> n;
	n++;
	std::vector<std::vector<int>> costs(n, std::vector<int> (n));
	std::vector<std::vector<int>> tracker(n, std::vector<int>(n));
	std::vector<std::vector<char>> directions(n-1, std::vector<char>(n-1));
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			if (i == n - 1 && j == n - 1)
			{
				break;
			}
			if (i < n - 1 && j < n-1)
			{
				std::cin >> directions[i][j];
			}
			else
			{
				std::cin >> costs[i][j];
			}
		}
	}
	int Q;
	std::cin >> Q;
	std::vector<std::pair<int, int>> flip (Q);
	for (int i = 0; i < Q; i++)
	{
		std::cin >> flip[i].first >> flip[i].second;
		flip[i].first--;
		flip[i].second--;
	}

	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			if (i < n - 1 && j < n - 1)
			{
				tracker[i][j] = 1;
			}
			
		}
	}
	for (int i = 0; i < n-1; i++)
	{
		for (int j = 0; j < n-1; j++)
		{
			if (directions[i][j] == 'R')
			{
				tracker[i][j + 1] += tracker[i][j];
			}
			else
			{
				tracker[i+1][j] += tracker[i][j];
			}
		}
	}
	std::cout << calc(costs, tracker) << std::endl;
	for (int x = 0; x < Q; x++)
	{
		int i = flip[x].first;
		int j = flip[x].second;
		tracker = adder(directions, tracker, -tracker[i][j], i, j);
		if (directions[i][j] == 'R')
			directions[i][j] = 'D';
		else
			directions[i][j] = 'R';
		tracker = adder(directions, tracker, tracker[i][j], i , j);
		std::cout << calc(costs, tracker) << std::endl;
	}

}
```
