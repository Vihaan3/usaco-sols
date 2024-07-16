# Pareidolia

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1328" %}

Attempt 1:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#define string std::string

string T;

int ending(int start)
{
	string target = "bessie";
	int t_idx = 1;
	for (int i = start + 1; i < T.size(); i++)
	{
		if (T[i] == target[t_idx])
		{
			t_idx++;
		}
		if (t_idx == 6)
		{
			return i;
		}
	}

	return -1;
}

int num_substrings(int start, int end)
{
	return (start + 1) * (T.size() - end);
}

int main()
{
	std::cin >> T;
	std::vector<int> bs;
	for (int i = 0; i < T.size(); i++)
	{
		if (T[i] == 'b')
		{
			bs.push_back(i);
		}
	}
	int total = 0;
	for (int start : bs)
	{
		int end = ending(start);
		if (end != -1)
		{
			total += num_substrings(start, end);
		}
	}
	std::cout << total;
}
```
