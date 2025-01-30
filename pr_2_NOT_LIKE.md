Practice 2 from the series.


**NOT LIKE** syntax example.

**%** is called wildcards.


Find job titles with
- Data or Business
- but not Data Senior/Senior Data


```sql

SELECT 
 	job_title AS position,
  job_location AS location, 
  salary_year_avg AS salary 
FROM 
 	job_postings_fact
WHERE 
    (job_title LIKE '%Business%' OR '%Data%') AND
     job_title LIKE '%Data%' AND job_title NOT LIKE '%senior%';

  ```

![Image](https://github.com/user-attachments/assets/9cb6d21b-ec9a-4879-9c65-90d267a05921)
