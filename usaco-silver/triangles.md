# Triangles

{% embed url="http://www.usaco.org/index.php?page=viewproblem2&cpid=1015" %}

This was a hard problem. I think a valuable lesson I learned here was to spend way more time playing with hand-made test cases on the whiteboard, and to spend more time on the whiteboard in general. I would've made every small logical breakthrough that I needed to get to the full solution if I'd just spent more time figuring it out on the whiteboard instead of staring at a screen and thinking.&#x20;

Pseudocode for the final solution:&#x20;

```
A struct fence that stores x, y, sum for bases, sum for heights
A vector fence of type fences
A vector for x-coords that's double the max input size and tracks (emphasis) y coordinates and indices
A vector for y-coords that's double the max input size and tracks (emphasis) x coordinates and indices
X-coords and y-coords will basically track y-coords for all positions along a specific x-coord/x-coords for all positions along a specifc y-coord

Take input into fences. Update xcoords and ycoords appropriately 
for all positions in x-coords:
    sort all positions along this x-coord
    find the heightsum for the first position naively
    loop through all the rest and find their heightsums using the recurrence relation (2i - n)(pos_i+1 - pos_i)
Ditto for y-coords but with basesum
Output the sum of (base_sum*height_sum) for each post + all the modification logic
```

Full solution:

```cpp
#include <iostream> 
#include <vector>
#include <algorithm>
#include <cmath>
#include <fstream>
#define ll long long

struct fence {
    ll x;
    ll y;
    ll height_sum;
    ll base_sum;
};

int main()
{

    ll n;
    std::ifstream fin("triangles.in");
    std::ofstream fout("triangles.out");
    fin >> n;
    std::vector<fence> fences(n);
    std::vector<std::vector<std::pair<ll, int>>> xcoords(2 * 10000);
    std::vector<std::vector<std::pair<ll, int>>> ycoords(2 * 10000);
    for (int i = 0; i < n; i++)
    {
        fin >> fences[i].x >> fences[i].y;
        fences[i].x += 10000;
        fences[i].y += 10000;
        xcoords[fences[i].x].push_back(std::make_pair(fences[i].y, i));
        ycoords[fences[i].y].push_back(std::make_pair(fences[i].x, i));
    }

    for (auto xcoord : xcoords)
    {
        if (xcoord.size() > 0)
        {
            std::sort(xcoord.begin(), xcoord.end());
            auto starter = xcoord[0];
            ll first_height_sum = 0;
            for (int i = 1; i < xcoord.size(); i++)
            {
                first_height_sum += xcoord[i].first - starter.first;
            }
            fences[starter.second].height_sum = first_height_sum;

            ll prev_height_sum = first_height_sum;
            auto prev = starter;
            for (int i = 1; i < xcoord.size(); i++)
            {
                fences[xcoord[i].second].height_sum = prev_height_sum + (2 * i - xcoord.size()) * (xcoord[i].first - prev.first);
                prev_height_sum = fences[xcoord[i].second].height_sum;
                prev = xcoord[i];
            }
        }
    }

    for (auto ycoord : ycoords)
    {
        if (ycoord.size() > 0)
        {
            std::sort(ycoord.begin(), ycoord.end());
            auto starter = ycoord[0];
            ll first_base_sum = 0;
            for (int i = 1; i < ycoord.size(); i++)
            {
                first_base_sum += ycoord[i].first - starter.first;
            }
            fences[starter.second].base_sum = first_base_sum;

            ll prev_base_sum = first_base_sum;
            auto prev = starter;
            for (int i = 1; i < ycoord.size(); i++)
            {
                fences[ycoord[i].second].base_sum = prev_base_sum + (2 * i - ycoord.size()) * (ycoord[i].first - prev.first);
                prev_base_sum = fences[ycoord[i].second].base_sum;
                prev = ycoord[i];
            }
        }
    }

    ll area = 0;
    for (auto fence : fences)
    {
        area += fence.height_sum * fence.base_sum;
    }

    fout << area % (1000000007) << std::endl;

}
```
