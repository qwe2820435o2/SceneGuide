# Why is redis sentinel cluster not working with only 2 nodes?

## 1. Reason
> Sentinel cluster must deploy more than 2 nodes

```markdown
If the Sentinel cluster deploys only 2 Sentinel instances, quorum=1

	+----+         +----+
	| M1 |---------| R1 |
	| S1 |         | S2 |
	+----+         +----+

```