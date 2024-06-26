# Range Reconstruction

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1256" %}

```cpp
#include <vector>
#include <iostream>
#include <limits.h>

int main()
{
	int n;
	std::cin >> n;
	std::vector < std::vector< int >> ranges (n, std::vector<int>(n));

	for (int i = 0; i < n; i++)
	{
		for (int j = i; j < n; j++)
		{
			std::cin >> ranges[i][j-i];
		}
	}

	std::vector<int> orig(n);
	for (int i = n - 2; i >= 0; i--)
	{
		orig[i] = orig[i+1] + ranges[i][1];
		int max = (-2147483647 - 1);
		int min = 2147483647;
		bool valid = true;
		for (int j = i; j < n; j++)
		{
			max = std::max(max, orig[j]);
			min = std::min(min, orig[j]);
			if (max - min != ranges[i][j-i])
			{
				valid = false;
			}
		}

		if (!valid)
		{
			orig[i] = orig[i + 1] - ranges[i][1];
		}
	}
	for (int i = 0; i < n; i++)
	{
		if (i != n - 1)
			std::cout << orig[i] << " ";
		else
			std::cout << orig[i];
	}
}
```
