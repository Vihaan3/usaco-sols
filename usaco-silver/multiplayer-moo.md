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
