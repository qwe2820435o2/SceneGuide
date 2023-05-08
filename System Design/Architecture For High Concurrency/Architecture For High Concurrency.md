# 1. Background

```
We encountered a situation where interface response times were becoming slower and slower due to high traffic volumes

This challenge was impacting the user experience and required a comprehensive optimization strategy
```

# 2. Basic Information
> How can we design a high-concurrency architecture?

**1. Who will use it?** 
```
Our users
```

**2. How will they use it?** 
```
They often listen to or download songs
```

**3. How many users do we have?**
```
Our monthly active users are more than 100 million
```

**4. What does the system do?**
```
We provide the functions that the music platform should have, like Spotify
```

**5. What are input and output of the system?**
```
The average value of the input is xxx Million bits per second
The maximum value of the input is xxx Million bits per second
The average value of output is xxx Million bits per second
The maximum value of output is xxx Million bits per second
```

**6. How many requests do we want to process per second?**
```
Current maximum requests are more than xx thousand per second
```

**7. What ratio of reads and writes do we want?**
```
10 to 1
```

# 3. How To Design