# Milk Sum

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1326" %}

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main()
{
	int N, Q;
	std::cin >> N;
	std::vector<int> vals (N);
	std::vector<int> indices(N);
	std::vector<int> multiplier(N);
	std::vector<int> pref (N+1);

	for (int i = 0; i < N; i++)
	{
		std::cin >> vals[i];
		indices[i] = i;
	}
	std::sort(indices.begin(), indices.end(), [&](int i, int j)
	{
		return vals[i] < vals[j];
	});

	std::sort(vals.begin(), vals.end());
	int T = 0;
	for (int i = 0; i < N; i++)
	{
		multiplier[indices[i]] = i;
		pref[i + 1] = pref[i] + vals[i];
		T += (i + 1) * vals[i];
	}

	std::cin >> Q;

	while (Q--)
	{
		int index, curr;
		std::cin >> index >> curr;
		index--;
		index = multiplier[index];

		int out = T;
		auto it = std::lower_bound(vals.begin(), vals.end(), curr);
		int new_index = std::distance(vals.begin(), it);
		if (curr > vals[index])
		{
			new_index--;
		}

		out = out - (index + 1) * vals[index];

		if (new_index >= index)
		{
			out -= (pref[new_index + 1] - pref[index + 1]);
		}

		else
		{
			out += (pref[index] - pref[new_index]);
		}
		out += (new_index + 1) * curr;
		std::cout << out << std::endl;
	}


}
```

