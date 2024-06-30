# Find and Replace

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1278" %}

Partial Sol:

```cpp
#include <vector>
#include <iostream>
#include <unordered_map>
#include <set>
#define umap std::unordered_map

void solve()
{
	std::string in, out;
	std::cin >> in >> out;
	std::vector<char> input, output;
	for (int i = 0; i < in.size(); i++)
	{
		input.push_back(in[i]);
		output.push_back(out[i]);
	}
	bool valid = true;
	umap <char, char> transforms;
	umap <char, std::vector<char>> undirected;
	umap <char, bool> checker;
	std::set <char> outset;
	for (auto outer : output)
		outset.insert(outer);
	if (outset.size() == 52 && output != input)
		valid = false;

	for (int i = 0; i < output.size(); i++)
	{
		if (transforms.find(input[i]) != transforms.end() && transforms[input[i]] != output[i])
			valid = false;
		transforms[input[i]] = output[i];
		undirected[input[i]].push_back(output[i]);
		undirected[output[i]].push_back(input[i]);
	}

	if (valid)
	{
		std::string Alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz";
		int num = 0;
		for (auto letter : Alphabet)
		{
			if (transforms.find(letter) != transforms.end() && transforms[letter] != letter)
			{
				num++;
				char current_letter = letter;
				std::vector<char> temp;
				while (true)
				{
					if (transforms.find(current_letter) != transforms.end() && checker.find(current_letter) == checker.end())
					{
						current_letter = transforms[current_letter];
						temp.push_back(current_letter);
						if (current_letter == letter)
						{
							num++;
							for (auto tp : temp)
							{
								checker[tp] = false;
							}
							break;
						}
						if (undirected[current_letter].size() > 2)
							break;
					}
					else
						break;
				}
			}
		}
		std::cout << num << std::endl;
	}
	else
		std::cout << -1 << std::endl;
}

int main()
{
	int n;
	std::cin >> n;
	while (n--)
		solve();
}
```
