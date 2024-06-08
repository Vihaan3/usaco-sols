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
