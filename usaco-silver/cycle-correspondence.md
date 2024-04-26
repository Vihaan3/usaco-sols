# Cycle Correspondence

### Problem-Solving

I completely misunderstood the problem statement, and ended up spending half an hour implementing the wrong thing (and it was a very inefficient solution as well).&#x20;

Real Solution

```cpp
#include <iostream>
#include <vector>
#include <set>
#include <algorithm>
#include <unordered_map>
#define umap std::unordered_map

int solve(std::vector <int> a, std::vector<int> b)
{
	umap <int, int> b1;
	for (int i = 0; i < b.size(); i++)
	{
		b1[b[i]] = i;
	}

	std::vector<int> counter(a.size());
	for (int i = 0; i < a.size(); i++)
	{
		auto it = b1.find(a[i]);
		if (it != b1.end())
		{
			int j = it->second;
			if (i >= j)
			{
				counter[i - j]++;
			}
			else
			{
				auto len = a.size();
				counter[i - j + len]++;
			}
		}
	}

	int max = 0;

	for (auto count : counter)
	{
		max = std::max(max, count);
	}
	return max;
}

int main()
{
	int n, k;
	std::cin >> n >> k;
	std::set<int> setter;
	std::vector<int> a(k);
	std::vector<int> b(k);

	for (int i = 0; i < k; i++)
	{
		std::cin >> a[i];
		setter.insert(a[i]);
	}
	for (int i = 0; i < k; i++)
	{
		std::cin >> b[i];
		setter.insert(b[i]);
	}

	auto outside_count = n - setter.size();
	auto b1 = b;
	std::reverse(b1.begin(), b1.end());
	//THIS MIGHT BE THE ISSUE. B1 MIGHT BE REFERENCING THE SAME THING
	std::cout << outside_count + std::max(solve(a, b), solve(a, b1));
}

```

Stupid Solution

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main()
{
	int n, k;
	std::cin >> n >> k;

	std::vector <int> a (k);
	std::vector <int> b(k);
	for (int i = 0; i < k; i++)
	{
		std::cin >> a[i];
	}
	for (int i = 0; i < k; i++)
	{
		std::cin >> b[i];
	}
	std::vector <std::pair <int, std::pair<int, int>>> a1 (k);
	std::vector <std::pair <int, std::pair<int, int>>> b1 (k);

	for (int i = 0; i < k; i++)
	{
		if (i == 0)
		{
			a1[0].first = a[0];
			a1[0].second.first = a[1];
			a1[0].second.second = a[k - 1];
			b1[0].first = b[0];
			b1[0].second.first = b[1];
			b1[0].second.second = b[k - 1];
		
		}
		else if (i == k - 1)
		{
			a1[k-1].first = a[k - 1];
			a1[k - 1].second.first = a[k - 2];
			a1[k - 1].second.second = a[0];
			b1[k - 1].first = b[k - 1];
			b1[k - 1].second.first = b[k-2];
			b1[k - 1].second.second = b[0];
		}
		else
		{
			a1[i].first = a[i];
			a1[i].second.first = a[i - 1];
			a1[i].second.second = a[i + 1];
			b1[i].first = b[i];
			b1[i].second.first = b[i - 1];
			b1[i].second.second = b[i + 1];
		}

	}

	std::sort(a1.begin(), a1.end());
	std::sort(b1.begin(), b1.end());
	std::vector<std::pair<bool, std::pair<int, int>>> a2 (n + 1);
	std::vector<std::pair<bool, std::pair<int, int>>> b2 (n + 1);
	
	auto mega = std::make_pair(a2, b2);
	for (int i = 0; i < k; i++)
	{
		auto ab = a1[i];
		auto ba = b1[i];
		mega.first[ab.first].first = true;
		mega.first[ab.first].second = ab.second;
		mega.second[ba.first].first = true;
		mega.second[ba.first].second = ba.second;
	}
	int count = 0;

	for (int i = 1; i < n + 1; i++)
	{
		auto ab = mega.first[i];
		auto ba = mega.second[i];
		if (ab.first == false && ba.first == false)
			count++;
		else if (ab.first == true && ba.first == true && ((ab.second.first == ba.second.first && ab.second.second == ba.second.second) || (ab.second.first == ba.second.second && ab.second.second == ba.second.first)))
			count++;
	}
	std::cout << count;
}


```

