# Question 1

给了一张表trip_info, 表中的列有\
rider_id (unique per rider), \
trip_id (unique per trip), \
trip_timestamp_utc (the UTC timestamp for when the trip began), \
and trip_status (can either be ‘completed’ or ‘not completed’).

table name | column name
--|--
uber_trip | rider_id , trip_id, begintrip_timestamp_utc, trip_status

写个query返回每个rider完成的第三个trip的trip_id。如果rider完成的trip不到3个，则排除。

最后问 Write a test query to validate the data in the resulting table. Indicate what you would expect the query to return if the data were valid

## Approach
There are two+ ways to write a query, which depends on the type of database:

**1) PostgreSQL, Oracle, etc (which support Common table expression):**

```javascript
with T1 as
(
select rider_id, trip_id, begintrip_timestamp_utc,
row_number() over (partition by rider_id order by begintrip_timestamp_utc asc) as r_n
from table
where trip_status = 'completed'
)

select T1.rider_id, T1.trip_id
from T1
where T1.r_n = 3
```

**2)Mysql: using stored procedure:**

```javascript
select T2.rider_id,T2.trip_id


(
select T1.rider_id,T1.trip_id,
@rank_sp := case when T1.rider_id = @rider_id_sp then @rank_sp + 1 else 1 end as r_n,
@rider_id_sp := T1.rider_id

from
(
select rider_id, trip_id, begintrip_timestamp_utc
from table
where trip_status = 'completed'
) T1

order by begintrip_timestamp_utc asc. 1point3acres

) T2


where T2.r_n = 3
```

最后的问题:
Write a test query to validate the data in the resulting table. Indicate what you would expect the query to return if the data were valid

主要测试SQL QA的能力。我的思路是，写个query 算出“有效且完成3个及以上trip 有多少个人"。

从第一题的答案table中，可以算出：
select count(*) as num_rider_3
from 第一题的返回table

从原table 可以算出：
```javascript
select sum(T1.cnt) as num_rider_3
(
select rider_id, count(1) as cnt
from table
where trip_status = 'completed'
group by rider_id
) T1
where T1.cnt > = 3
```
如果两个结果一致，说明正确。
不一致，说明不正确。

