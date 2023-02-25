# Large table splitting smooth migration steps

## 1. Question
> Before we start, let's consider these questions

```
1. How to synchronize stock data of old table to new table?
2. How to confirm that the data is complete?

```

## 2. Whole process
> The overall process is divided into 4 steps.As follows:

![Large table splitting smooth migration steps](../../Material/image/Large%20table%20splitting%20smooth%20migration%20steps%20—%20Whole%20Process.png)

## Detail


### Data verifying program
> Set the step size, 10000 as a batch

1. Query the same batch of ID data in the new table and the old table
2. Generate MD5 values for the data in the new table and the old table respectively
3. Compare their MD5 values, if they are the same, compare the next batch; if they are different, compare the details one by one
4. The detailed comparison is to traverse the MD5 values of each record in the batch and compare their MD5 values
5. Find out the id whose MD5 value comparison fails and record it to the specified file

### Program double writting
> Double write is used to replace incremental synchronization of cannel

1. Adds, deletes and modifies operations on the old table must be written to the new table
2. After the double write goes online, stop the incremental synchronization of the canvas

### Program query switch
> Prepare for emergency failback with configuration center setup switches

Step by step switch to new lookup table according to business priority

### Verify that queries are all toggled
> Monitor the sql statement to know whether all businesses are quering the new table

sql monitoring for tables