# Connecting Two Barns

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1159" %}

Attempt 1

I made a very basic mistake in trying to solve this problem. I based all of my thinking around the sample test case, and the sample test case was _very_ weak and misleading. Usually, I'm able to catch myself because I try to test out solutions on hand-made test cases before implementation but in this case my thinking was so heavily based off the sample test case that all the hand-made test cases I made looked like the sample test case.&#x20;

The glaring hole in my mental model of the problem was the fact that I assumed that all the connected components had to be consecutive numbers, which was insanely stupid. With that constraint, the problem was so trivial that I instantly knew the solution and spent several minutes trying to figure out what I was missing (because there was no way it could be _this_ easy). Then, hubris kicked in and I decided that maybe it felt easy because I was improving and I decided to implement anyways.  Needless to say, the implementation was very off.&#x20;
