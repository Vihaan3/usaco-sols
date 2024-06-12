# Circular Barn

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1255" %}

I had literally no idea how to do this problem until I read the solution. One of the hardest problems I've come across.

```
SOLUTION PSEUDO-CODE

Pre-compute all primes
For each test case:
    Take in input as a vector of room
    int max = 1e9;
    For room in rooms:
        int moves = 0;
        if room is even:
            moves = room/2;
        else:
            find the largest prime number less than room such that they both have the same value when %4ed
            moves = (room - prime)/2 + 1
        if moves / 2 < max /2:
            max = moves
    if moves is even:
        std:: cout << "Farmer John" << std::endl;
    else:
        std::cout << "Farmer Nhoj" << std::endl;
```

```cpp
#include <iostream>
#include <vector>

std::vector<bool> composite(5000005, false);

int i = 2; 

void primer()
{
	while (i * i <= composite.size()) {
		if (!composite[i]) { 
			for (int j = i * i; j <= composite.size(); j += i) { 
				composite[j] = true;
			}
		}
		i += 1;
	}
}


void solve()
{
	int n;
	std::cin >> n;
	std::vector<int> rooms(n);
	for (int i = 0; i < n; i++)
	{
		std::cin >> rooms[i];
	}

	int max = 1e9;
	int moves = 0;

	for (auto room : rooms)
	{
		if (room % 2 == 0)
		{
			moves = room / 2;
		}
		else
		{
			auto old = room;
			while (composite[room])
			{
				room-=4;
			}

			moves = (old - room) / 2 + 1;
		}
		if (moves / 2 < max / 2)
		{
			max = moves;
			
		}
	}
	if (max % 2 == 1)
	{
		std::cout << "Farmer John" << std::endl;
	}
	else
		std::cout << "Farmer Nhoj" << std::endl;
}

int main()
{
	int n;
	std::cin >> n;
	primer();
	while (n--)
	{
		solve();
	}
}
```
