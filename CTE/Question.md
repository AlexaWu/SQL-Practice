Member can make purchase via either mobile  or desktop platform. Using the following data table to determine the total number of member and revenue for mobile-only, desktop_only and mobile_desktop..

The input spending table is

member_id|    date|    channel|   spend
--|--|--|--
1001|    1/1/2018|    mobile|    100
1001|    1/1/2018|    desktop|    100
1002|    1/1/2018|    mobile|    100
1002|    1/2/2018|    mobile|    100
1003|    1/1/2018|    desktop|    100
1003|    1/2/2018|    desktop|    100

The output data is

date|    channel|    total_spend|    total_members
--|--|--|--
1/1/2018|    desktop|    100|    1
1/1/2018|    mobile|    100|    1
1/1/2018|    both|    200|    1
1/2/2018|    desktop|    100|    1
1/2/2018|    mobile|    100|    1
1/2/2018|    both|    0|    0

思路是先得出不同date和不同user的distinct channel个数table, 然后得出total_spend and total_members for unique combination of user_id and spend_date, 最后利用cross join强制显示出来distinct date, 和不同channel的表格去left join上面的表格。学习到了crossjoin! ~经过好几个test case,可以run出正确结果（显示both是0的情况）
```javascript
SELECT d.spend_date, c.channel,
  coalesce(total_spend,0) as total_spend
  coalesce(total_members,0) as total_members
FROM
(select distinct spend_date from spending) d
cross join
(select 'both' as channel union select 'mobile' union select 'desktop') c
left join
(SELECT a.spend_date,
     CASE WHEN chn_count=2 then 'both'
     ELSE channel
     END
     as channel,
     sum(spend) as total_spend, 
     count(distinctauser_id) as total_members
FROM spending a
inner join
(SELECT user_id, spend_date, count(distinct channel) as chn_count
FROM spending
group by user_id, spend_date) b 
using(user_idspend_date)
group by spend_date 
  CASE WHEN chn_count=2
  then 'both'
  ELSE channel
  END) data
using(spend_datechannel)
```
