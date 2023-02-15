# Link Of The Sending

## 1. Triggered Time
```
When the function is triggered, it should call the counting interface

Example：

Here is a playlist

We can collect, download, play, share, comment and other operations on it

At this time, the counting of the business will be triggered
```


## 2. Common Data Format
**DTO：**
> According to the tableType, fieldType abstract mapping to the corresponding queue route, data table, field

```
class SendReq
	Integer tableType		//table
	Integer fieldType		//field
	Integer itemId			//primary Id
	Integer count			//count
```

**Enum：**

> Store the specific data of the mapping

```
enum RoutingTypeEnum
	//col route key
	//music route key
	//video route key
	...
```

```
enum TableTypeEnum
	//col table
	//music table
	//video table
	...
```

```
enum FieldTypeEnum
	//collect field
	//comment field
	//share field
	//stream field
	//download field
	...
```


## 3. Asynchronous Processing
> Decoupling using message queues

![Counting Design (2) - Asynchronous Processing](../../Material/image/Counting%20Design%20(2)%20-%20Asynchronous%20Processing.png)