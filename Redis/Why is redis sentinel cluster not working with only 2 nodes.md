# Why is redis sentinel cluster not working with only 2 nodes?

## 1. Reason
> Sentinel cluster must deploy more than 2 nodes

```
If the Sentinel cluster deploys only 2 Sentinel instances, quorum=1

	+----+         +----+
	| M1 |---------| R1 |
	| S1 |         | S2 |
	+----+         +----+

Configuration: quorum = 1

The master is down, as long as there is one sentinel in s1 and s2 that the master is down, it can be switched over. At the same time, a sentinel will be elected in s1 and s2 to perform the failover.

At the same time, majority is required, that is, most sentinels are running

The majority of 2 sentinels is 2 (majority=2 for 2, majority=2 for 3, majority=3 for 5, and majority=2 for 4). 

If both sentinels are running, failover can be performed.

But if the entire machine running on M1 and S1 goes down, then there is only one sentinel left

At this point there is no majority to allow failover to be performed, although there is an R1 on the other machine, the failover will not be performed

```