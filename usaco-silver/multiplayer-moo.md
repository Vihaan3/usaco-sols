# Multiplayer Moo

My initial pseudocode (idk if it would've fully worked because I didn't implement it due to how gnarly and complicated I imagine the implementation will be - there is probably some pesky side case I'm missing):

```
Go through all cells and set any that aren't connected to 0.
Go through all cells and keep track of counts (while traversing, multiply by -1 once you've left a cell so that you know not to double count if you need to come back that way).
Return the max count
Go through all cells and keep track of the regions that don't have at least one 0 connected to them. 
Go through all cells and figure out which regions connect
Return the Max(Max of the connected regions vs (Max of the regions that connect to at least one 0 + 1))  
```

This is definitely not optimized code, but I think it would be easiest to write and fastest to implement this way.&#x20;