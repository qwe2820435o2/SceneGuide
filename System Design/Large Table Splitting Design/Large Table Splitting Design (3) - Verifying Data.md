# Verifying Data
> Set the step size, 10000 as a batch

1. Query the same batch of ID data in the new table and the old table
2. Generate MD5 values for the data in the new table and the old table respectively
3. Compare their MD5 values, if they are the same, compare the next batch; if they are different, compare the details one by one
4. The detailed comparison is to traverse the MD5 values of each record in the batch and compare their MD5 values
5. Find out the id whose MD5 value comparison fails and record it to the specified file
