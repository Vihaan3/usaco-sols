# Painting Fence Posts

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1423" %}

My First Solution

{% code overflow="wrap" %}
```
direct simulation 
construct the fence:
	find the highest point and use recursion from there. Each point will have one vertical fence and one horizontal fence. 
create a counter for each post
for each cow:
	find the shorter route:
		recurse down both of the 2 directions (if it's at a post horizontal and vertical, if it's along a horizontal line left and right, if it's on a vertical line up and down)
		any time the cow brushes past a fence, increment the counter
	set the counters to the numbers for the shorter route
```
{% endcode %}

Official Solution

{% code overflow="wrap" %}
```
Use a dictionary of lists to store a list of posts along all horizontal and vertical lines that have posts. Sort each list at the end

Starting at a random fence, traverse until you get back to the starting fence.
During this traversal:
- renumber the posts and store the mapping between the original posts
- keep track of the total distance traveled from the starting post for each post (and at the end calculate the total perimeter of the fence). 

For each cow:
    - binary search on the x and y axes to find the fence segment that it is on. Use that to determine how far it will have to travel. If that distance is greater than the perimeter/2, traverse the opposite direction. 
    - use a difference array to store the changes for the range of posts the cow will touch

End:
prefix sum the difference array
use the mapping to print out how many times each post will get touched
```
{% endcode %}
