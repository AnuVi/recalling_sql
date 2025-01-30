Practice 1 from the series.
Find jobs:
- in Boston or Anythere
- job-name is Data Analyst and salary is over 100 000
- job-name is Business Analyst and salary is over 70 000

**IN** - to look for multiple values in WHERE-clause.





```sql

SELECT 
 	job_title_short, job_location, salary_year_avg 
FROM 
 	job_postings_fact
WHERE 
 	job_location IN ('Boston, MA', 'Anywhere') AND
    (
    	(job_title_short = 'Data Analyst' AND salary_year_avg > 100000) OR
	(job_title_short = 'Business Analyst' AND salary_year_avg > 70000)
    )
ORDER BY 
	salary_year_avg DESC;

```


![Image](https://github.com/user-attachments/assets/563bcfe0-aee2-4451-a843-f44cd5e44789)

