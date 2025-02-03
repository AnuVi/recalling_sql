Practice 8 from series.

```sql

-- Find job postings from the first quarter that have a salary greater than 70K
SELECT 
	job_title_short,
	job_location,
	job_via,
	job_posted_date::DATE,
	salary_year_avg,
	round(salary_year_avg/12,2) AS per_month,
	round(salary_year_avg/12/160, 2) AS per_hour

FROM (SELECT
	  *
    FROM
    	january_jobs
    UNION ALL
    SELECT
    	*
    FROM
    	february_jobs
    UNION ALL
    SELECT
    	*
    FROM
    	march_jobs) AS I_quarter_jobs
     
WHERE I_quarter_jobs.salary_year_avg > 70000
AND (job_location like '%Estonia%' OR 
	job_location like '%Finland%'OR 
	job_location like '%Latvia%' OR 
	job_location like '%Lithuania%')
ORDER BY I_quarter_jobs.salary_year_avg DESC
```
![Image](https://github.com/user-attachments/assets/8f89440f-08cc-4091-8f39-c1e1c6bc1170)
