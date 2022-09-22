# Evolution process of millions ip libraries design
> Purchased millions of IP libraries provided by third parties and provided them in the form of database files *.mmdb

## Stage 1: Load the Ip local database file provided by the third party when the project starts

**Issue:**
1. The library file is large, and the loading consumes memory
2. The library file is placed in the project, which increases the size of the package body

## Stage 2: Extract the IP database file to an external shared folder

**Advantages:** reduce the size of the package body, and share a piece of data for multiple projects

**Issue:** Still consumes a lot of memory after loading










