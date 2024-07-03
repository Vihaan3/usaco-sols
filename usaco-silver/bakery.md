# Bakery

{% embed url="https://usaco.org/index.php?page=viewproblem2&cpid=1302" %}

Steps to solving:

* Binary search for the minimum number of moonies paid _p_ that will satisfy the constraints.&#x20;
  * (_C_ is the original time per cookie and _M_ is the original time per muffin. _c_ and _m_ are the respective new times.)
  * Constraints:&#x20;
    * &#x20;both _c_ and _m_ need to be between 1 and their _C, M_ respectively
    * &#x20;_c_ + _m_ = _C_ + _M - p_
    * The values _c_ and _m_ should satisfy all of Bessie's friends&#x20;
  * To pass all test cases, the hardest part is to find whether there are _c_s and _m_s that satisfy the constraints for a given _p_ without brute forcing over all possible values.&#x20;
