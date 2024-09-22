# Multiplayer Moo

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=836" %}

My initial pseudocode (idk if it would've fully worked because I didn't implement it due to how gnarly and complicated I imagine the implementation will be - there are probably some pesky edge cases I'm missing):

```
Go through all cells and set any that aren't connected to 0.
Go through all cells and keep track of counts (while traversing, multiply by -1 once you've left a cell so that you know not to double count if you need to come back that way).
Return the max count
Go through all cells and keep track of the regions that don't have at least one 0 connected to them. 
Go through all cells and figure out which regions connect
Return the Max(Max of the connected regions vs (Max of the regions that connect to at least one 0 + 1))  
```

This is definitely not optimized code, but I think it would be easiest to write and fastest to implement this way.&#x20;

The official solution was actually somewhat similar (at least for the beginning). I was basically doing a convoluted flood fill, which is what the official solution recommended. After the flood fill, the official solution compresses regions to single nodes for time efficiency, which is something I hadn't thought of.&#x20;



Attempt 2.0

I attempted to try this problem again from scratch \~a month after first trying it and ended up writing a solution that was almost the exact same as the official one w/o even realizing it.  Either I'm getting good enough that I'm starting to think on the right wavelength, or there were traces of the right solution in my memory. It's definitely more the latter but hopefully a mix of both.&#x20;

This is a near-complete solution. It's only missing the last \~20 lines of code needed to find the result for 2 numbers (I've figured out single and compression). &#x20;

```
#include <vector>
#include <iostream>
#include <algorithm>

int id = -1;
int max_size = 0;
int row_num;
int col_num;
const int MAX_N = 250;
bool visited[MAX_N][MAX_N];  
std::vector<int> cc_sizes;
std::vector<int> id_to_num;
std::vector <std::vector<std::pair<int, int>>> grid;
std::vector<std::vector<int>> cc_connect;

void floodfill(int r, int c, int number, bool first) {
	if ((r < 0 || r >= row_num || c < 0 || c >= col_num) 
		|| grid[r][c].first != number                           
		|| visited[r][c]                                 
		)
	{
		max_size = std::max(max_size, cc_sizes[id]);
		return;
	}

	if (first)
	{
		id++;
		cc_sizes.push_back(0);
		id_to_num.push_back(number);
	}
	visited[r][c] = true;  
	grid[r][c].second = id; 
	cc_sizes[id]++;

	floodfill(r, c + 1, number, false);
	floodfill(r, c - 1, number, false);
	floodfill(r - 1, c, number, false);
	floodfill(r + 1, c, number, false);
}

int main()
{
	int n;
	std::cin >> n;
	row_num = n;
	col_num = n;
	// MAKE SURE THIS WORKS
	grid = std::vector <std::vector<std::pair<int, int>>> (n, std::vector<std::pair<int, int>> (n));

	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			std::cin >> grid[i][j].first;
		}
	}

	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			floodfill(i, j, grid[i][j].first, true);
		}
	}
	
	std::cout << max_size << std::endl;

	cc_connect = std::vector<std::vector<int>> (cc_sizes.size());
	
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			int curr_id = grid[i][j].second;
			int curr_size = cc_sizes[curr_id];
			std::vector<std::pair<int, int>> adders = { {0, 1}, {0, -1}, {1, 0}, {-1, 0} };

			for (auto adder : adders)
			{
				int i_hat = i + adder.first;
				int j_hat = j + adder.second;

				if (i_hat == n || i_hat < 0 || j_hat == n || j_hat < 0)
				{
					break;
				}

				if (grid[i_hat][j_hat].second != curr_id)
				{
					cc_connect[curr_id].push_back(grid[i_hat][j_hat].second);
					cc_connect[grid[i_hat][j_hat].second].push_back(curr_id);
				}
			}
		}
	}

}
```
