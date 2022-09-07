# Three ways to batch update

## Regular Bulk Update

```mysql
UPDATE video v
SET v.stream = 8571
WHERE
	v.id IN (
		10000,
		10001,
		10002,
		10003,
		10004,
		10005
	)
```

This is the most commonly used batch update method, but it has the disadvantage that it can only set fixed values

When each of our id corresponds to a different stream, this method does not apply

## Bulk update with intermediate table


## InsertOrUpdate method batch update



