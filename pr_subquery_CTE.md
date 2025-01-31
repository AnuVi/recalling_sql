# SUBQUERY
SELECT, FROM, WHERE CLAUSES

```sql
-- only jobs posted in January
SELECT *
FROM ( --SUBQ. start
    SELECT * FROM job_postings_fact
    WHERE EXTRACT (month FROM job_posted_date) = 1
) AS january_jobs --SUBQEND

```
![Image](https://github.com/user-attachments/assets/72075a40-c76d-4a35-a467-7fa13ddf2684)


```sql
-- job offers without degree
SELECT name, company_id 
FROM company_dim
WHERE company_id IN (
    SELECT company_id
    FROM job_postings_fact
    WHERE job_no_degree_mention = TRUE
    LIMIT 6
)
```
![Image](https://github.com/user-attachments/assets/e39708ba-a43a-4e09-ba3f-9106c0a91cb7)

# CTE 

- CTE: common table expressions
- SELECT, INSERT, UPDATE, DELETE

  
```sql
-- job postings from February

WITH february_jobs AS ( -- CTE start
 SELECT * FROM job_postings_fact
    WHERE EXTRACT (month FROM job_posted_date) = 2

) -- CTE end

SELECT * FROM february_jobs LIMIT 10;
```
![Image](https://github.com/user-attachments/assets/2f997e6a-c5c7-446f-8fd8-9204e379b51b)

```sql
-- how many ads per total for company as posts and company name are in different tables

WITH company_ad AS(
    SELECT company_id, count(job_id) AS ads_total
    FROM job_postings_fact
    GROUP BY company_id
)

SELECT company_dim.name AS company_name,
	   company_ad.ads_total
FROM company_dim
LEFT JOIN company_ad
  ON company_dim.company_id =company_ad.company_id
ORDER BY company_ad.ads_total DESC
LIMIT 200;
```

![Image](https://github.com/user-attachments/assets/0d2fb29b-7e54-48df-b36d-69626b500478)

