Different DATE-functions and practice 5 from series.

# DATE

- as string
  
```sql

SELECT '2023-03-12';
```
![Image](https://github.com/user-attachments/assets/ef7ab788-b9d5-455c-a0fa-6dab0fd0e78b)


# ::DATE

- !NB used in Postgres
  - in MySql use CAST/CONVERT
      - SELECT job_posted_date, CAST(job_posted_date AS DATE) AS job_posted_date_converted FROM job_postings_fact LIMIT 6;
- used if we only want DATE
- at the moment we have job_posted_date as TIMESTAMP (yyyy-mm-dd HH:mm:ss)
- 

  
```sql

SELECT job_posted_date, job_posted_date::DATE
FROM job_postings_fact
LIMIT 6;
```
![Image](https://github.com/user-attachments/assets/30a3c5eb-1e45-42ca-8ae8-1d8d693de075)


# TIMEZONES

- As we don't have any info about TIMEZONES in DB we have to say it twice. 
- As machine TIMEZONE and the TIMEZONE we want to go.
- https://www.postgresql.org/docs/7.2/timezones.html 

```sql
SELECT
  job_title_short, job_location,job_posted_date, 
  job_posted_date AT TIME ZONE 'UTC' AT TIME ZONE 'EST'
FROM job_postings_fact
LIMIT 6;
```

![Image](https://github.com/user-attachments/assets/eb8e1b47-1470-45af-9161-162c6dd08ab8)

# EXTRACT

- EXTRACT part of the time/date - e.g only hours

  
```sql

SELECT
  job_title_short, job_location,job_posted_date, 
  EXTRACT (month from job_posted_date) as Month
FROM job_postings_fact LIMIT 6;

```

![Image](https://github.com/user-attachments/assets/3a683e41-f870-4022-a816-b650de45482a)

-- Useful if we want to see trends according to e.g. months

```sql
SELECT
  count(job_id) as job_ads_per_month, 
  EXTRACT (month from job_posted_date) as date_month
FROM
  job_postings_fact WHERE job_title_short = 'Data Analyst'
GROUP BY date_month
ORDER BY date_month ASC

```
![Image](https://github.com/user-attachments/assets/67e2f3e1-4fb6-4db8-aee4-18fc7b31b043)
