
also where salary_year_avg data is missing
all together 132 postings
the only 5 job postings

SELECT 
	job_title,
    job_title_short
    job_id,
    job_location,
    name,
    salary_year_avg,
    job_posted_date
 FROM 
 	job_postings_fact
LEFT JOIN company_dim ON
      (company_dim.company_id = job_postings_fact.company_id)
WHERE job_location IN ('Estonia', 'Lithuania', 'Latvia', 'Finland') 
    AND job_title_short LIKE '%Analyst%'
    AND salary_year_avg IS NOT NULL

![Image](https://github.com/user-attachments/assets/23b19515-9b2a-410b-a4c3-9ad71d622163)

-- From which country most postings
SELECT 
  job_title_short,
  job_location,
  count(job_id) as jobs_per_country
FROM job_postings_fact
WHERE job_location IN ('Estonia', 'Lithuania', 'Latvia', 'Finland') 
    AND job_title_short LIKE '%Analyst%'
GROUP BY job_location, job_title_short
ORDER BY jobs_per_country DESC

![Image](https://github.com/user-attachments/assets/5bbd7d41-e9e8-4e75-a50a-4d89038c6860)

-- from which portal 
SELECT 
  job_location,
  job_via,
  -- count(job_id) as jobs_per_country,
  count(job_via) as postings_per_portal
FROM job_postings_fact
WHERE 
     job_location IN ('Estonia', 'Lithuania', 'Latvia', 'Finland') 
  -- (job_location LIKE '%Estonia%' OR  job_location LIKE  '%Lithuania%'
   -- OR  job_location LIKE '%Latvia%' OR  job_location LIKE '%Finland%'
  -- )
    AND job_title_short LIKE '%Analyst%'
GROUP BY job_via, job_location
ORDER BY job_location, postings_per_portal DESC
![Image](https://github.com/user-attachments/assets/8389c2c7-ee4d-4151-be41-fe3d0eeca16b)


-- From which company
SELECT 
  job_location,
  name,
  -- count(job_id) as jobs_per_country,
  count(name) as postings_per_company
FROM job_postings_fact
LEFT JOIN company_dim ON
      (company_dim.company_id = job_postings_fact.company_id)
WHERE 
     job_location IN ('Estonia', 'Lithuania', 'Latvia', 'Finland') 
  -- (job_location LIKE '%Estonia%' OR  job_location LIKE  '%Lithuania%'
   -- OR  job_location LIKE '%Latvia%' OR  job_location LIKE '%Finland%'
  -- )
    AND job_title_short LIKE '%Analyst%'
GROUP BY job_location, name
ORDER BY postings_per_company DESC
![Image](https://github.com/user-attachments/assets/7b44d25e-fd9a-43cd-8a62-95eb7038bbb1)
![Image](https://github.com/user-attachments/assets/4b4c6592-399e-4175-9e47-440dfb284fae)
