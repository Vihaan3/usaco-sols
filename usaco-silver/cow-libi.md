# Cow-libi

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1303" %}

Attempt 1: (I'm not quite sure why it doesn't work)

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <math.h>
#include <stdlib.h>


bool check(std::pair<int, std::pair<int, int>> alibi, std::pair<int, std::pair<int, int>> grazing)
{
	int a = grazing.second.first - alibi.second.first;
	int b = grazing.second.second - alibi.second.second;
	int c = (a * a + b * b);
	int d = (alibi.first - grazing.first);
	d *= d;
	return c <= d;

}

int main()
{
	int G, N;
	std::cin >> G >> N;
	std::vector<std::pair<int, std::pair<int, int>>> alibis (N);
	std::vector<std::pair<int, std::pair<int, int>>> grazings(G);
	for (int i = 0; i < G; i++)
	{
		std::cin >> grazings[i].second.first >> grazings[i].second.second >> grazings[i].first;
	}
	for (int i = 0; i < N; i++)
	{
		std::cin >> alibis[i].second.first >> alibis[i].second.second >> alibis[i].first;
	}
	std::sort(alibis.begin(), alibis.end());
	std::sort(grazings.begin(), grazings.end());
	int innocent = 0;
	for (int i = 0; i < grazings.size(); i++)
	{
		while (alibis.size() > 0 and alibis[0].first < grazings[i].first)
		{
			bool valid = true;
			valid = valid && check(alibis[0], grazings[i]);
			if (i != 0)
			{
				valid = valid && check(alibis[0], grazings[i-1]);
			}
			if (!valid)
			{
				innocent++;
			}
			alibis.erase(alibis.begin());
		}

		if (i == grazings.size() - 1)
		{
			while (alibis.size() > 0)
			{
				if (!(check(alibis[0], grazings[i])))
				{
					innocent++;
				}
				alibis.erase(alibis.begin());
			}
		}
	}
	std::cout << innocent;
}
```
