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

#### 2.2.1 Points 1 and 2 cases

**Points 1 and 2 are just to alleviate the problem, but in fact it does not solve the problem in the end, because the gateway is still a hindsight**

![Points 1 and 2 cases](../Material/image/Gateway%20dynamic%20sensing%20service%20goes%20online%20and%20offline%20—%20Points%201%20and%202%20cases%20analysis.png)

#### 2.2.2 Points 3 case

**The third point is actually the practice of common registration centers on the market, but zookeeper lacks the online and offline service management function compared to other registration centers, and we need to implement it ourselves**

![Points 3 cases](../Material/image/Gateway%20dynamic%20sensing%20service%20goes%20online%20and%20offline%20—%20Points%203%20case%20analysis.png)

#### 2.2.3 Points 4 case

**Point 4, the change is relatively large, there is a certain risk, and it takes more time to complete**

![Points 4 cases](../Material/image/Gateway%20dynamic%20sensing%20service%20goes%20online%20and%20offline%20—%20Points%204%20case%20analysis.png)

## 3. Implementation in the industry
> Comparing the implementation of the dynamic perception service of the Nacos registration center of the Ali system

![Implementation in the industry](../Material/image/Gateway%20dynamic%20sensing%20service%20goes%20online%20and%20offline%20—%20Implementation%20in%20the%20industry.png)

## 4. Design

### 4.1 Case one

![Case one](../Material/image/Gateway%20dynamic%20sensing%20service%20goes%20online%20and%20offline%20—%20Case%20one.png)

#### 4.1.1 Event direction

```markdown

1. Before deployment, notify the configuration service about the node about to be published, and then the publishing thread sleeps for 20 seconds
2. Save the node information and current timestamp of the service to the configuration center
3. The gateway receives the node information of the service in near real time, and performs traffic screening on the node
4. Continue with automated publishing. When the release is successful, the service will register the node information with Zookeeper
5. Listen to the node generation event of zookeeper
6. When an event is monitored, notify the gateway to unblock the node of the blocked traffic

```

#### 4.1.2 Compensation measures
> Due to the weak reliability of zookeeper event monitoring, an additional compensation measure is required
