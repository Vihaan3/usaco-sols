# Cow Frisbee

Partly inspired by the official sol.&#x20;

````cpp
#include <bits/stdc++.h>
using namespace std;

long long sum (vector<pair<int, int>> heights)
{
	sort(heights.begin(), heights.end(), greater<pair<int, int>>());
	set<int> order;
	long long ans = 0;
	for (int i = 0; i < heights.size(); i++)
	{
		auto iterator = order.insert(heights[i].second);
		auto it = iterator.first;
		if (next(it) != order.end())
		{
			ans += (*next(it)) - (*it) + 1; 
		}
	}
	return ans;
}

int main() {
	int n;
	cin >> n;
	vector <pair<int, int>> heights (n);
	for (int i = 0; i < n; i++)
	{
		cin >> heights[i].first;
		heights[i].second = i;
	}
	long long ans = 0;
	ans += sum(heights);
	for (int i = 0; i < n; i++)
	{
		heights[i].second = n - 1 - i;
	}
	ans += sum(heights);
	cout << ans;
}	
```
````

