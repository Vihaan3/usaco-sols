# Closest Cow Wins

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1158" %}

**Attempt 1**

```
#include <iostream>
#include <vector>
#include <algorithm>
#define ll long long

int main()
{
	ll K, M, N;
	std::cin >> K >> M >> N;	
	std::vector<std::pair<ll, ll>> patches (K+M);
	for (ll i = 0; i < K; i++)
	{
		std::cin >> patches[i].first >> patches[i].second;
	}
	for (ll i = K; i < K+M; i++)
	{
		std::cin >> patches[i].first;
		patches[i].second = -1;
	}
	std::vector<ll> values;

	std::sort(patches.begin(), patches.end());
	ll curr_interval = 0;
	ll one_cow_best = 0;
	bool first = true;
	for (ll i = 0; i < patches.size(); i++)
	{
		if (patches[i].second == -1)
		{
			if (first)
			{
				values.push_back(curr_interval);
				first = false;
			}
			else
			{	
				if (curr_interval - one_cow_best == 26)
				{
					bool v = true;
				}
				values.push_back(curr_interval - one_cow_best);
			}
			curr_interval = 0;
			one_cow_best = 0;
			ll interval_begin = patches[i].first;
			ll interval_end = 0;
			ll half = 0;
			for (ll j = i; j < patches.size(); j++)
			{
				if (patches[j].second == -1)
				{
					interval_end = patches[j].first;
					break;
				}
			}
			// Might be an error here
			half = (interval_end - interval_begin) / 2;
			ll one_cow_curr = 0;
			ll k = i + 1;
			for (ll j = i + 1; j < interval_end; j++)
			{
				while (k < interval_end && (patches[k].first - patches[i].first) < half)
				{
					one_cow_curr += patches[k].second;
					k++;
				}
				one_cow_best = std::max(one_cow_best, one_cow_curr);
				one_cow_curr -= patches[j].second; 
			}
			if (one_cow_best == 26)
			{
				bool v = true;
			}
			values.push_back(one_cow_best);
		}

		else
		{
			curr_interval += patches[i].second;
		}
	}
	values.push_back(curr_interval);
	std::sort(values.begin(), values.end(), std::greater<ll>());

	ll taste = 0;
	for (ll i = 0; i < std::min(N, ll(values.size())); i++)
	{
		taste += values[i];
	}
	std::cout << taste;
}
```
