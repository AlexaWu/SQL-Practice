# [Question](https://www.hackerrank.com/challenges/interviews/problem)

## correct
```javascript
select 
  contests.contest_id, 
  contests.hacker_id, 
  contests.name,
  sum(submissions_sums.sum_submissions),
  sum(submissions_sums.sum_accepted_submissions),
  sum(views_sums.sum_views),
  sum(views_sums.sum_unique_views)
from contests 
join colleges on contests.contest_id = colleges.contest_id
join challenges on colleges.college_id = challenges.college_id

#subquery to get total sums for the Submission stats.
#these subqueries use left joins, so that the unrelated/empty information is not joined.
left join 
(select challenge_id,
  sum(total_submissions) as sum_submissions,
  sum(total_accepted_submissions) as sum_accepted_submissions
  from submission_stats 
  group by challenge_id) 
as submissions_sums
on challenges.challenge_id = submissions_sums.challenge_id

#another subquery to get total sums for Views stats
left join
(select 
  challenge_id,
  sum(total_views) as sum_views,
  sum(total_unique_views) as sum_unique_views
  from view_stats group by challenge_id) 
as views_sums
on challenges.challenge_id = views_sums.challenge_id

#group the information per-contest so that everything is aggregated.
group by contests.contest_id, contests.hacker_id, contests.name

#HAVING works like WHERE, except over aggregations, which is what we want here.
having (
  sum(submissions_sums.sum_submissions) +
  sum(submissions_sums.sum_accepted_submissions) +
  sum(views_sums.sum_views) +
  sum(views_sums.sum_unique_views)
) > 0
order by contests.contest_id;
```

## incorrect
```javascript
select Contests.contest_id, 
    hacker_id, 
    name, 
    sum(total_submissions), 
    sum(total_accepted_submissions), 
    sum(total_views), 
    sum(total_unique_views)
from Contests 
join Colleges on Contests.contest_id = Colleges.contest_id
join Challenges on Colleges.college_id = Challenges.college_id
join View_Stats on Challenges.challenge_id = View_Stats.challenge_id
join Submission_Stats on View_Stats.challenge_id = Submission_Stats.challenge_id
group by Contests.contest_id, hacker_id, name
having sum(total_submissions) + sum(total_accepted_submissions) + sum(total_views) + sum(total_unique_views) !=0
order by Contests.contest_id asc;
```
