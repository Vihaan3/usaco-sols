# Moo Route

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1280" %}

```cpp
#include <vector>
#include <iostream>
#include <string>

int main()
{
	int n;
	std::cin >> n;
	std::vector<int> cross(n+1);
	for (int i = 0; i < n; i++)
	{
		std::cin >> cross[i];
	}

	int i = 0;
	std::string out;

	while (true)
	{
		if (i == 0 && cross[0] == 0)
		{
			break;
		}

		while (cross[i] > 0)
		{
			cross[i]--;
			i++;
			out.append("R");
		}

		while (i > 0 && (cross[i - 1] >= 2 || cross[i] <= 0))
		{
			i--;
			cross[i]--;
			out.append("L");
		}
	}

	std::cout << out;
}
```
