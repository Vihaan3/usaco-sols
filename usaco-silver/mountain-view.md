# Mountain View

{% embed url="http://www.usaco.org/index.php?page=viewproblem2&cpid=896" %}

### Problem-Solving

I figured out basically everything I needed to fully solve the problem pretty early on, but I couldn't figure out the crucial final step and ended up taking a peek at the solution. Next time, I probably should just stick to it for a little longer. I also need to learn to simplify solutions somewhat. I was wondering how to graph each triangle in a 2d grid, but I completely missed the fact that I just needed the starting and end points, which I'd already figured out how to find. The simplest viable approach is definitely the best approach, and I should build up from there if it doesn't work.

### Implementation

_I re-programmed the solution \~30 minutes after reading the solution in-depth so it has many similarities._

```cpp
#include <iostream>
#include <vector>
#include <fstream>
#include <algorithm>

struct Mountain 
{
	int begin;
	int end;
};

bool operator < (const Mountain& m1, const Mountain& m2)
{
	if (m1.begin == m2.begin)
		return m1.end > m2.end;
	return m1.begin < m2.begin;
}

int main() {
	std::ifstream read("mountains.in");
	int mountain_num;
	read >> mountain_num;
	std::vector<Mountain> mountains (mountain_num);
	for (int i = 0; i < mountain_num; i++)
	{
		int x, y;
		read >> x >> y;
		mountains.push_back({ x - y, x + y });
	}

	std::sort(mountains.begin(), mountains.end());

	int rightmost = -1;
	int visible_num = 0;
	for (const Mountain& m : mountains) {
		if (m.end > rightmost) {
			visible_num++;
			rightmost = m.end;
		}
	}

	std::ofstream("mountains.out") << visible_num << std::endl;
}
```
