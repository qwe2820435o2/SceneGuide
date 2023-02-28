# Double Writting
> Double write is used to replace incremental synchronization of cannel

1. Adds, deletes and modifies operations on the old table must be written to the new table
2. After the double write goes online, stop the incremental synchronization of the canvas