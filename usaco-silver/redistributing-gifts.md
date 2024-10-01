# Redistributing Gifts

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1206" %}

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

Official solution: The official solution is really elegant and simple. The fact that I couldn't figure it out probably points to my severe weakness with graph problems in general.&#x20;

This is the pseudocode for it:&#x20;

```
Take in input up to the gift that each cow has and ignore the rest
Loop through each cow:
    Dfs to find every single cow that this cow connects to 
        reachable[og_cow][new_cow] = 1 
Loop through all cows:
    Loop through the gifts:
        if (reachable[gift][cow] == 1)
            print (gift)
```

Attempt 2: I made the same mistake again over a month later :(. The only reason I was able to catch myself was that I mentally simulated my implementation on a hand-made sample test case before jumping into the implementation and realized that I wasn't doing it right. \
&#x20;
