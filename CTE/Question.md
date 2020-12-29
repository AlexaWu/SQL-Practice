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

思路是先得出不同date和不同user的distinctchannel个数table,然后得出total_spendandtotal_membersforuniquecombinationofuser_idandspend_date,最后利用crossjoin强制显示出来distinctdate,和不同channel的表格去leftjoin上面的表格。学习到了crossjoin!之前从来没用过我觉得这样看逻辑很容易理解~经过好几个testcase可以run出正确结果（显示both是0的情况）
```javascript
SELECT d.spend_date c.channel,
  coalesce(total_spend,0) as total_spend
  coalesce(total_members,0) as total_members
FROM
(select distinct spend_date from spending) d
cross join
(select 'both' as channel union select'mobile'unionselect'desktop') c
left join
(SELECTaspend_dateCASEWHENchn_count=2then'both'ELSEchannelENDaschannelsum(spend)astotal_spendcount(distinctauser_id)astotal_membersFROMspendingacheck1point3acres
formoreinnerjoin(SELECTuser_idspend_datecount(distinctchannel)aschn_countFROMspendinggroupbyuser_idspend_date)busing(user_idspend_date)groupbyspend_dateCASEWHENchn_count=2then'both'ELSEchannelEND)datausing(spend_datechannel)
```
