# Convention 2

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=859" %}

### Problem-Solving

I figured out the problem pretty quickly; I think it's probably time to start moving to average difficulty problems

### Implementation

It was a pretty straight-forward solution but I wasted a lot of time debugging.&#x20;

```
// FUNDAMENTALLY CORRECT BUT UNOPTIMIZED SOLUTION
#include <vector>
#include <fstream>
#include <iostream>
#include <algorithm>
//#define fin std::cin 
//#define fout std::cout 

int main()
{
	std::ifstream fin ("convention2.in");
	int n;
	fin >> n;
	std::vector <std::pair<std::pair<int, int>, int>> store (n);
	for (int i = 0; i < n; i++)
	{
		fin >> store[i].first.first >> store[i].first.second;
		store[i].second = i;
	}

	std::sort(store.begin(), store.end());
	std::vector <std::pair<std::pair<int, int>, int>> que;
	int max = 0;
	int current = 0;
	que.push_back(store[0]);
	store.erase(store.begin());
	while (true)
	{
		if (store.size() == 0 && que.size() == 0)
			break;
		if (store.size() > 0 && current == store[0].first.first)
		{
			auto temp = store[0];
			store.erase(store.begin());
			bool valid = false;
			for (int i = 0; i < que.size(); i++)
			{
				if (temp.second < que[i].second && i != 0)
				{
					que.insert(que.begin() + i, temp);
					valid = true;
					break;
				}
			}
			if (!valid)
				que.push_back(temp);
		}

		if (que.size() > 0 && que[0].first.first + que[0].first.second == current)
		{
			que.erase(que.begin());
			if (que.size() > 0)
			{
				max = std::max(max, current - que[0].first.first);
				que[0].first.first = current;
			}
		}

		current++;
	}
	std::ofstream fout("convention2.out");
	fout << max;
}
// FULLY CORRECT SOLUTION
#include <algorithm>
#include <cstdio>
#include <iostream>
#include <set>
#include <vector>

using namespace std;

int main() {
	freopen("convention2.in", "r", stdin);
	freopen("convention2.out", "w", stdout);

	int cow_num;
	vector<vector<int>> cows;
	cin >> cow_num;
	for (int c = 0; c < cow_num; c++) {
		int start, duration;
		cin >> start >> duration;
		cows.push_back({c, start, duration});
	}

	// sort by arrival time
	auto cmp = [](const vector<int> &a, const vector<int> &b) {
		return a[1] < b[1];
	};
	sort(cows.begin(), cows.end(), cmp);

	int time = 0;
	int curr = 0;
	int longest_wait = 0;

	// sorted by priority so that the highest seniority starts eating first
	set<vector<int>> waiting;
	// as long as we haven't processed all cows or there are still cows waiting
	while (curr < cow_num || !waiting.empty()) {
		// this cow can be processed.
		if (curr < cow_num && cows[curr][1] <= time) {
			waiting.insert(cows[curr]);
			curr++;
			// no cow waiting, skip to the next cow.
		} else if (waiting.empty()) {
			// set time to the ending time of the next cow.
			time = cows[curr][1] + cows[curr][2];
			curr++;
		} else {
			// process the next cow
			vector<int> next = *waiting.begin();
			longest_wait = max(longest_wait, time - next[1]);

			// set the time to when this cow finishes
			time += next[2];
			waiting.erase(waiting.begin());
		}
	}

	cout << longest_wait << endl;
}
```
