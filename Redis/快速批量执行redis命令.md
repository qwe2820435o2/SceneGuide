# 1. 背景

使用redis的时候，经常会有这么一个需求：批量删除某前缀的key

怎么做呢？



# 2. 处理方式一



## 2.1 准备好需要删除的key

为了避免阻塞redis，最好不要用keys命令进行检索，可以使用scan命令得到keys，如下：

```
./redis-cli -h 192.168.22.1 -p 6379 --scan --pattern 'user*'
```



## 2.2 批处理拼接del命令

可以借用notepad++的批处理命令，Alt + Shift 拼接del，效果如下：

```
del user:10086
del user:5566
del user:10010
```

最后将该txt文本命名为：temp_20211113.txt



## 2.3 批处理key

执行如下命令：

```
cat temp_20211113.txt | redis-cli -h 192.168.22.1 -p 6379 
```

# 3. 处理方式二

```
./redis-cli -h 192.168.22.1 -p 6379 -c --scan --pattern 'user:*'  |  xargs -r -t -n1 ./redis-cli -h 192.168.22.1 -p 6379 -c del
```

