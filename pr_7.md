Practice 7 from series.

```sql
-- find job_ads count per skills
-- display top 10 skills - skill_id, count and posting per skill

WITH skills_listing AS (
SELECT skill_id, count(skill_id) as demand_for_skill 
FROM skills_job_dim AS sjd
INNER JOIN job_postings_fact AS jpf
ON sjd.job_id = jpf.job_id
WHERE jpf.job_title_short = 'Data Analyst'
AND jpf.job_work_from_home = true
GROUP BY skill_id
)

SELECT skills_dim.skill_id, skills_dim.skills, skills_listing.demand_for_skill FROM skills_dim
INNER JOIN skills_listing
 ON skills_dim.skill_id = skills_listing.skill_id
ORDER BY skills_listing.demand_for_skill DESC 
LIMIT 10

```

![Image](https://github.com/user-attachments/assets/3fc403c1-b52b-4ad3-8f26-b3c78c715de4)
