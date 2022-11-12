# Gateway dynamic sensing service goes online and offline

## 1. Foreword

### 1.1 Current Situation

```markdown

Due to historical issues, the registry of our project still uses Zookeeper

Compared with other registries, this component is relatively native and lacks operation and maintenance management, so it can only be implemented by itself

```

### 1.2 Direction

```markdown

The gateway dynamically senses the service going offline

The key is to know in advance which instance is about to go offline, and then route traffic to other instances in advance

```

## 2. How to implement

### 2.1 Current feasibility

```markdown

1. Reduce the gateway synchronization registry time interval and increase the instance cache synchronization frequency                difficulty level：★
2. Monitor Zookeeper temporary node change events, and actively refresh the instance cache                                            difficulty level：★★
3. Actively notify the gateway to offline an instance in advance                                                                      difficulty level：★★✰
4. Change the registration center to form, use the off-the-shelf implementation scheme                                                difficulty level：★★★✰

```

### 2.2 Case analysis

**Points 1 and 2 are just to alleviate the problem, but in fact it does not solve the problem in the end, because the gateway is still a hindsight**

![Jemalloc memory](../Material/image/Gateway%20dynamic%20sensing%20service%20goes%20online%20and%20offline%20—%20Points%201%20and%202%20cases%20analysis.png)
