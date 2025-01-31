-- CREATE TABLES for Jan/Feb/Mar

```sql
CREATE TABLE january_jobs AS
    SELECT * 
    FROM job_postings_fact
    WHERE EXTRACT(month FROM job_posted_date)=1
```

```sql

CREATE TABLE february_jobs AS
    SELECT * 
    FROM job_postings_fact
    WHERE EXTRACT(month FROM job_posted_date)=2;
```

```sql

CREATE TABLE march_jobs AS
    SELECT * 
    FROM job_postings_fact
    WHERE EXTRACT(month FROM job_posted_date)=3;

```

```sql

SELECT * FROM march_jobs LIMIT 2;

```
![Image](https://github.com/user-attachments/assets/146f2014-ab4d-4978-ad75-e21cb55a790d)
