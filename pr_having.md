# HAVING 
Goes between GROUP BY and ORDER BY

```sql
SELECT 
	job_title,
    job_location AS location,
    salary_year_avg AS salary
 FROM 
 	job_postings_fact
 WHERE salary_year_avg IS NOT NULL
 group by job_title, job_location, salary_year_avg
 HAVING job_title LIKE 'Bi%'
 ORDER BY salary DESC
```
![Image](https://github.com/user-attachments/assets/a4b8cb44-7c29-4ba1-bdd5-c47ac518143f)


```sql
SELECT 
    job_title,
	count (distinct (job_title)) as position,
    avg(salary_year_avg) AS salary,  
	job_location
 FROM 
 	job_postings_fact
 WHERE 
 	job_location LIKE '%Estonia%'
GROUP BY job_title, job_location;
```
![Image](https://github.com/user-attachments/assets/91c098bd-eb3d-4705-8563-d030508d2c1d)

Verison also:
![Image](https://github.com/user-attachments/assets/dde2dff9-4b47-4cab-af31-5c3a0f06bd29)



