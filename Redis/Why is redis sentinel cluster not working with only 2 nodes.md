# Why is redis sentinel cluster not working with only 2 nodes?

## 1. Reason
> Sentinel cluster must deploy more than 2 nodes

```markdown
If the Sentinel cluster deploys only 2 Sentinel instances, quorum=1

	+----+         +----+
	| M1 |---------| R1 |
	| S1 |         | S2 |
	+----+         +----+

Configuration: quorum = 1

The master is down, as long as there is one sentinel in s1 and s2 that the master is down, it can be switched over. At the same time, a sentinel will be elected in s1 and s2 to perform the failover.

```