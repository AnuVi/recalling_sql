# JOINS

In series where used:
- LEFT JOIN all records from left table (table1) and matching rows from right table (table2).
- RIGHT JOIN all records from right table (table2) and matching rows from left table (table1).
- INNER JOIN data is there in both tables

# LEFT JOIN

```sql
SELECT
	jpf.job_title,
	jpf.job_location,
    -- jpf.company_id,
    --  cd.company_id,
    cd.name,
    jpf.salary_year_avg,
    (jpf.salary_year_avg/12) AS per_month,
    (jpf.salary_year_avg/12/160) AS per_hour
FROM job_postings_fact as jpf
LEFT JOIN company_dim as cd
     -- how these tables are connected, all content from LEFT table and matching from the right side
     ON cd.company_id=jpf.company_id
WHERE jpf.job_location LIKE '%Estonia%';

```

![Image](https://github.com/user-attachments/assets/504dc29a-de53-4361-a98e-0cfb2d1d4153)

# RIGHT JOIN 

Should be also done - to check irregularities.

# INNER JOIN

```sql
SELECT
	jpf.job_title,
	jpf.job_location,
   -- jpf.job_id,
    -- sjd.job_id,
	sd.skills
FROM job_postings_fact as jpf
INNER JOIN skills_job_dim as sjd 
	ON jpf.job_id = sjd.job_id
INNER JOIN skills_dim as sd
	ON sd.skill_id = sjd.skill_id
WHERE jpf.job_location LIKE '%Estonia%';

```
![Image](https://github.com/user-attachments/assets/35c5d99c-e7f1-4caf-b350-c389f15e6d99)
