# 1. background

When using redis, there is such a requirement that delete keys of a prefix in batches

How to do it?



# 2. Processing method one



## 2.1 Prepare the key that needs to be deleted

In order to avoid blocking redis, it is best not to use the keys command to retrieve the keys

We can use the scan command to get the keys, as follows:

```
./redis-cli -h 192.168.22.1 -p 6379 --scan --pattern 'user*'
```



## 2.2 Batch splice del command

You can borrow the batch command of notepad++

Alt + Shift splicing del 

The effect is as follows:

```
del user:123456
del user:789
del user:5566
```

Finally name the txt text as：temp_20211113.txt



## 2.3 batch handle key

Execute the following command：

```
cat temp_20211113.txt | redis-cli -h 192.168.22.1 -p 6379 
```

# 3. Processing method two

```
./redis-cli -h 192.168.22.1 -p 6379 -c --scan --pattern 'user:*'  |  xargs -r -t -n1 ./redis-cli -h 192.168.22.1 -p 6379 -c del
```

# 4. Processing method three

Batch setting a short expiration time can also indirectly play the role of deletion

```
redis-cli -h 192.168.22.1 -p 6379 -c --scan --pattern 'user:*'  |  xargs -i redis-cli -h 192.168.22.1 -p 6379 expire {} 10
```

