# Cowlendar

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1376" %}

This problem was subtly tricky. I was insanely confused at how one would even begin tackling the problem because I was taking a naive approach to time complexity analysis. &#x20;

```cpp
// For some reason, this doesn't work on several test cases even though it feels perfect to me. Still debugging it
#include <set>
#include <vector>
#include <iostream>
#include <algorithm>
#include <cmath>

int N;
int sum = 0;
std::vector <int> vec;
int min;

void calc(int L)
{
	if (L > min)
	{
		return;
	}

	bool valid = true;
	std::set<int> mods;
	for (int v : vec)
	{
		mods.insert(v%L);
		if (mods.size() >= 4)
		{
			valid = false;
			break;
		}
	}
	if (valid)
		sum += L;
}

int main()
{
	std::set<int> months;

	std::cin >> N;
	std::cin >> min;
	months.insert(min);
	for (int i = 1; i < N; i++)
	{
		int a;
		std::cin >> a;
		min = std::min (min, a);
		months.insert(a);
	}
	for (std::set<int>::iterator it = months.begin(); it != months.end(); ++it) {
		vec.push_back(*it);
	}
	min /= 4;

	if (vec.size() < 4)
	{
		for (int i = 1; i <= min; i++)
		{
			sum += i;
		}
		std::cout << sum;
		return 0;
	}
	std::set<int> nums;
	for (int i = 0; i < 4; i++)
	{
		for (int j = i + 1; j < 4; j++) 
		{
			int diff = std::abs(vec[i] - vec[j]);
			for (int k = 1; k < (int)sqrt(diff) + 1; k++)
			{
				if (diff % k == 0) 
				{
					nums.insert(k);
					nums.insert(diff / k);
				}
			}
		}
	}

	for (auto k : nums)
	{
		calc(k);
	}

	std::cout << sum;
}
```
