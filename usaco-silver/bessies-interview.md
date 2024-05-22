# Bessie's Interview

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1422" %}

This was a fun problem because it was the first time in quite a while (maybe even since I started moving on from easy Silver problems) that I think I figured out a complete algorithm.

{% code overflow="wrap" %}
```
My Algorithm
- keep a queue with all of the upcoming interviews, sorted in increasing order of how long before it ends. Delete the interviews from the input array as they get processed into the queue
- jump up the minutes by the first position in the queue and subtract everything else in the queue by that
- if multiple elements in the queue are now the same, they can be combined into one (but you need some way of also denoting how many farmers each number represents)
- for the first element, choose the minimum of the next F numbers (where F is the number of farmers this number represents). Delete the first element from the queue and add that minimum to the queue. Delete those interviews from the input array
```
{% endcode %}

{% code overflow="wrap" %}
```
Official Algorithms 
Solution 1:
**events** are instances of multiple farmers finished interviews at the same time
Simulate the process forward through time, storing **events** as they occur. 
Define Ei to be the set of farmers in the i-th event.
After all N cows have been processed, create a set S of Bessie's possible interviewers. Initially, S={x}.
Process the events backward through time, and if S∩Ei≠∅, then update S=S∪Ei

Solution 2:
Like solution 1, but instead of tracking **events**, construct a directed graph with vertices for times, and a directed edge between each cow's start time and end time. Run bfs or dfs from Bessie's start time to determine which farmers make it there. 
```
{% endcode %}
