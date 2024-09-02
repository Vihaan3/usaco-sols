# Subsequences Summing to Sevens

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=595" %}

This was a really easy problem and my solution ended up matching the official solution quite closely (I swear I didn't cheat). I found that it took me way too long to implement anyway relative to the difficulty, and I think it's because I tend to zone out a little bit when I know I'm working on an easy implementation which is something I need to fix. I probably spent 10 minutes longer than I should've implementing this problem (took me 20 minutes when it would've taken 10 or less if I'd been more focused).&#x20;

```
#include <iostream>
#include <fstream>
#include <vector>
#include <algorithm>

#define ll long long

int main()
{
	ll n;
	std::ifstream fin("div7.in");
	std::ofstream fout("div7.out");
	fin >> n;
	std::vector <ll> arr(n);
	for (ll i = 0; i < n; i++)
	{
		fin >> arr[i];
	}

	std::vector <ll> prefix (n+1);
	for (ll i = 0; i < n; i++)
	{
		prefix[i + 1] = prefix[i] + arr[i];
		prefix[i + 1] %= 7;
	}
	std::vector <ll> short(7);
	std::vector <ll> long(7);
	
	for (ll i = 1; i < n+1; i++)
	{
		if (short[prefix[i]] == 0)
		{
			short[prefix[i]] = i;
		}
		long[prefix[i]] = i;
	}
	ll max = 0;
	for (ll i = 1; i < 7; i++)
	{
		max = std::max(max, long[i] - short[i]);
	}
	fout << max;
}
```
