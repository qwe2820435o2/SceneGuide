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

```mysql
UPDATE
  video v
  INNER JOIN temp_video_stream tvs ON v.id = tvs.video_id
SET
  v.stream = tvs.stream
```

Relying on the intermediate table to update can also achieve the purpose of batch update

It also has disadvantages, that is: the intermediate table needs to be borrowed, and the intermediate table data must be cleared in advance when the next update is required.


## InsertOrUpdate method batch update

```mysql
insert into video (id, stream)
        values
<foreach collection="videoList" item="video" index="index" separator=",">
		(#{video.id}, 0)
</foreach>
on duplicate key update
stream = stream + values(stream)
```

The most recommended batch update method is this

It neither needs to borrow the intermediate table, but also achieves the purpose of updating the stream corresponding to the id



