# CASE 
Similar to programming *if*.

Job_location should be 
- if Estonia - local
- if Anythere - remote
-  otherwise - onsite

```sql

SELECT job_id, job_location, job_title_short,
    CASE 
        WHEN job_location LIKE '%Estonia%' THEN 'local'
        WHEN job_location = 'Anywhere' THEN 'remote'
        ELSE 'onsite'
    END AS location_category
 FROM job_postings_fact
 ORDER BY location_category ASC
LIMIT 1000;
```

![Image](https://github.com/user-attachments/assets/ea26a587-c258-4c0b-bc54-197650d93b74)




```sql
-- how many jobs available based on location local, remote, onsite

SELECT count(job_id),
    CASE 
        WHEN job_location LIKE '%Estonia%' THEN 'local'
        WHEN job_location = 'Anywhere' THEN 'remote'
        ELSE 'onsite'
    END AS location_category
 FROM job_postings_fact
 GROUP BY location_category
```

![Image](https://github.com/user-attachments/assets/13d0c2c6-42bb-4b45-b98f-08b896c473ce)
