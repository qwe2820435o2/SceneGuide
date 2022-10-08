# Evolution process of millions ip libraries design
> Purchased millions of IP libraries provided by third parties and provided them in the form of database files *.mmdb

## Stage 1: Load the Ip local database file provided by the third party when the project starts

**Issue:**
1. The library file is large, and the loading consumes memory
2. The library file is placed in the project, which increases the size of the package body

## Stage 2: Extract the IP database file to an external shared folder

**Advantages:** reduce the size of the package body, and share a piece of data for multiple projects

**Issue:** Still consumes a lot of memory after loading

## Stage 3: Extract the IP database data to the redis
> draw on the B+ tree structure to design the structure of level 1 index, level 2 index, and level 3 pointing to the final data

**Advantages:** No need to pay attention to the local Ip library file, only deal with the redis cache

**Issue:** 

Excessive concentration of hot data and high concurrency will lead to a high number of tcp links on a redis node

The phenomenon reflected in the client is an error: could not get a resource from the pool


## Stage 4: Increase local cache, cache hotspot IP, carry concurrent

**Advantages:** Reduced 70% of ip requests to redis, and the number of tcp connections is stable

**Issue:** The remaining 30% traffic still occupies a certain number of tcp links


## Stage 5: Follow-up optimization ideas

Level 1 and level 2 indexes are placed in the local cache, which can effectively reduce the number of links to redis