# Redistributing Gifts

Attempt 1: Very stupidly, I misread the problem statement as "after _each_ reassignment, every cow ends up with the same gift as she did originally, or a gift that she prefers over the one she was originally assigned" instead of "after reassignment". This made me approach the problem from the perspective of a sequence of  "trades" that have to strictly be mutually beneficial rather than plain reassignment. &#x20;

```cpp
#include <iostream>
#include <vector>

int main()
{
	int n;
	std::cin >> n;
	n = n + 1;
	std::vector<int> ctog (n);
	std::vector<int> gtoc(n);
	std::vector <std::vector<int>> wishlists(n, std::vector<int> (n));
	for (int i = 1; i < n; i++)
	{
		for (int j = 1; j < n; j++)
		{
			std::cin >> wishlists[i][j];
		}
		ctog[i] = i;
		gtoc[i] = i;
	}
	for (int i = 1; i < n; i++)
	{
		int curr_i_gift = ctog[i];
		bool found = false;

		for (int j = 1; j < n; j++)
		{
			int curr_j_gift = wishlists[i][j];
			if (curr_j_gift == curr_i_gift)
			{
				break;
			}
			int trader = gtoc[curr_j_gift];
			for (int k = 1; k < n; k++)
			{
				int curr_k_gift = wishlists[trader][k];
				if (curr_k_gift == curr_j_gift)
				{
					break;
				}
				if (curr_k_gift == curr_i_gift)
				{	
					ctog[i] = curr_j_gift;
					gtoc[curr_j_gift] = i;
					ctog[trader] = curr_i_gift;
					gtoc[curr_i_gift] = trader;
					found = true;
					break;
				}
			}
			if (found)
			{
				break;
			}
		}
	}

	for (int i = 1; i < n; i++)
	{
		std::cout << ctog[i] << std::endl;
	}

}
```

\
&#x20;
