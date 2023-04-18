# Optimization Detail

## 1. Security

**Old Uri:** 

```
mongodb://{ip}:{port}/{database}?connectTimeoutMS=4000&serverSelectionTimeoutMS=5000&minConnectionsPerHost=50&connectionsPerHost=100
```

**New Uri:**

```
mongodb://{username}:{passport}@{ip}:{port}/{database}?connectTimeoutMS=4000&serverSelectionTimeoutMS=5000&minConnectionsPerHost=50&connectionsPerHost=100&readPreference=secondaryPreferred
```