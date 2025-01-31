# Union
Combines results from two or more SELECT statements: have to have same amount columns and data type.

```sql
-- let's combine t.january_jobs and t.february_jobs and_march_jobs

SELECT
	job_title_short,
	company_id,
	job_location
FROM
	january_jobs
UNION
SELECT
	job_title_short,
	company_id,
	job_location
FROM
	february_jobs
UNION
SELECT
	job_title_short,
	company_id,
	job_location
FROM
	march_jobs
```

![Image](https://github.com/user-attachments/assets/57de2907-ddd7-42fa-9ad6-f405920f87ba)

# UNION ALL
Gets rid of duplicate rows.
