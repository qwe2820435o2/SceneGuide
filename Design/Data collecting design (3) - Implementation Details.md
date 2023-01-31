

# Implementation Details

## 1. Behavior Collecting

### 1.1 Upload Time

```markdown
Due to network differences, the client will be divided into offline reporting and real-time reporting

In the case of a weak network, report offline, that is: store locally, and report in batches when the network is smooth

When the network is good, report directly in batches
```

### 1.2 Prevent Duplicate Upload

```markdown
The daily data volume of behavioral buried points is too large to perform real-time deweighting, which will affect the performance

Therefore, data is stored first, and T+1 deweighting is performed on the big data side
```

### 1.3 Data Format

**Format:**

```markdown
Request： POST      application/x-www-from-urlencoded

{
    "commonParams":{
        "extend_data":"",
        "os":"android",
        "lan":"en",
        "imei":"89fc9bcffcb84959",
        "imsi":"4ac123bcb615a5dc"
    },
    "events":"7615ffdbbb1f4e5f9b55ad010852848b"
}
```

**Field Description:**

|    Field Name    |                     Desc                     | Type |
| :----------: | :------------------------------------------: | :----: |
| commonParams |             Public parameter, JSON string              | String |
|    events    | Dot product information JSONArray data, Compressed | String |


### 1.4 Data Compress

```
You can use the corresponding compression algorithm according to the actual situation, such as Gzip, lz4, snapy, etc.
```

## 2. Business Collecting

### 2.1 Upload Time

```
When the business operation is executed successfully, the data is reported
```

### 2.2 Prevent Duplicate Upload

```
Involving business, real-time deduplication is required, and big data T+1 deduplication cannot be used

Consider using Bloom filters for deduplication
```

### 2.3 Data Format

```
Because it involves the consumption of many different businesses, there is no restriction on the format

It is controlled by the business itself, but it must follow the development specification
```

### 2.4 Data Compress

```
You can use the corresponding compression algorithm according to the actual situation, such as Gzip, lz4, snapy, etc.
```





