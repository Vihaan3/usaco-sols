# February 2024 Practice Contest

Comfortable Cows:

I got the general idea for the solution as I hand-solved the input test cases and did the coding relatively fast as well. Then I spent an hour debugging because the code fails on all but 2 test cases. I still don't know why, but board\_counts seems to occassionally be 3 even when it should be 4.

```
/*
So basically you want to:
- keep track of the state of the game board (just an int 
table with 0, 1, 2 for off, on-normal, on-added)
- have a separate map that's a copy of the game board but an int
representing the number of adjacent cows
- for loop through all the cows to be added:
	process(position, bool)
	print out num_additions

def process(position, is_return)
	if the cow already exists and is on-normal: 
		minus minus from the num_additions variable
	else
		add the cow at that position, if is_return than 1 else 2
		num_additions++;
		check all 4 directons:
			edit their game board copy
				if their game board copy is now at 3:
					process(find_fourth(pos), is_return=false)
			edit this pos' game board copy
				if it is now at 3:
					process(find_fourth(pos), is_return=false)

def find_fourth(position):
	find fourth position, accounting for boundaries and things
	like that

*/

#include <bits/stdc++.h>
using namespace std;
#define ll long long 

int SIZE = 5000;
int num_additions = 0;
std::vector<std::vector<int>> board(SIZE, std::vector<int>(SIZE));
std::vector<std::vector<int>> board_counts(SIZE, std::vector<int>(SIZE));

pair<int, int> find_fourth(pair<int, int> position)
{
	int x = position.first; int y = position.second;
	pair<int, int> directions[] = { {1, 0},{-1, 0},{0, 1},{0, -1} };
	for (auto direction : directions)
	{
		int a = direction.first + x; int b = direction.second + y;
		cout << a << " "  << b << " " << board[a][b] << endl; 
		if (a >= 0 and b >= 0 and a < SIZE and b < SIZE and board[a][b] == 0)
		{
			return make_pair(a, b);
		}
	}
	throw runtime_error("No valid fourth position found!");
	return make_pair(-1, -1);
}

void process(pair<int, int> position, bool is_return)
{
	int x = position.first; int y = position.second;
	if (board[x][y] == 2)
	{
		num_additions--;
	}

	else
	{
		board[x][y] = (is_return) ? 1 : 2;
		if (!is_return) num_additions++;
		pair<int, int> directions[] = { {1, 0},{-1, 0},{0, 1},{0, -1} };
		for (auto direction : directions)
		{
			int a = direction.first + x; int b = direction.second + y;
			if (a >= 0 and b >= 0 and a < SIZE and b < SIZE and board[a][b] > 0)
			{
				board_counts[x][y]++;
				board_counts[a][b]++;
				if (board_counts[a][b] == 3)
				{
					auto p = find_fourth(make_pair(a, b));
					if (p.first != -1 and p.second != -1)
						process(p, false);
				}
			}
			if (board_counts[x][y] == 3)
			{
				auto p = find_fourth(position);
				if (p.first != -1 and p.second != -1)
					process(p, false);
			}
		}
	}
}

int main() {
	int n;
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		int x, y;
		cin >> x >> y;
		x += 3000, y += 3000;
		process(make_pair(x, y), true);
		cout << num_additions << endl;
	}
}
```

