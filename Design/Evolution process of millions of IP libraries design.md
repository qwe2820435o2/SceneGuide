# Evolution process of millions of IP libraries design
> Purchased millions of IP libraries provided by third parties and provided them in the form of database files *.mmdb

## Stage 1: Load the Ip local database file provided by the third party when the project starts

**Issue:**
1. The library file is large, and the loading consumes memory
2. The library file is placed in the project, which increases the size of the package body

## Stage 2: Extract the IP database file to an external shared folder

**Advantages:** reduce the size of the package body, and share a piece of data for multiple projects

**Issue:** Still consumes a lot of memory after loading

## Stage 3: Extract the IP database data to the Redis
> draw on the B+ tree structure to design the structure of the level 1 index, level 2 index, and level 3 points to the final data

**Advantages:** No need to pay attention to the local Ip library file, only deal with the Redis cache

**Issue:** 

Excessive concentration of hot data and high concurrency will lead to a high number of TCP links on a Redis node

The phenomenon reflected in the client is an error: could not get a resource from the pool


## Stage 4: Increase local cache, cache hotspot IP, and carry concurrent

**Advantages:** Reduced 70% of IP requests to Redis, and the number of TCP connections is stable

**Issue:** The remaining 30% of traffic still occupies a certain number of TCP links


## Stage 5: Follow-up optimization ideas

Level 1 and level 2 indexes are placed in the local cache, which can effectively reduce the number of links to Redis