# Intro
[Luke Barousse](https://www.lukebarousse.com/) collects data from job-posts: [https://datanerd.tech/](https://datanerd.tech/). During his SQL-course <em>data from year 2023</em> is used.

I've decided to focus my research on Estonia, Latvia, Lithuania and Finland because:
- I have a personal connection with this region
- and I am looking around "data-<em>fill with suitbale the position</em>" job-market


# Job Postings And Avarage Salary

All together there were 132 job postings:
- located in Estonia or Latvia or Lithuania or Finland
- and where job title consisted word "Analyst"
- unfortunatley only 5 of them had info about salary per year
  
![Image](https://github.com/user-attachments/assets/23b19515-9b2a-410b-a4c3-9ad71d622163)  

```sql
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
```


# Job Postings And Country
If to look posts according to the country and the job title had word "Analyst" in it, Finland was leading with 96 offers. Estonia had 21, Lithuania 13 and Latvia had only 2 job-ads.

![Image](https://github.com/user-attachments/assets/5bbd7d41-e9e8-4e75-a50a-4d89038c6860)

```sql
SELECT 
  job_title_short,
  job_location,
  count(job_id) as jobs_per_country
FROM job_postings_fact
WHERE job_location IN ('Estonia', 'Lithuania', 'Latvia', 'Finland') 
    AND job_title_short LIKE '%Analyst%'
GROUP BY job_location, job_title_short
ORDER BY jobs_per_country DESC
```
Short job-titles with word "Analyst" did not offer any suprises: data analyst, business analyst + variation with "senior". However, it is more interesting to look at longer job titles. From team leading and being a data architect to internships, 99 different job titles were mentioned. 

![image](https://github.com/user-attachments/assets/439f9e83-e059-47d4-b48c-308c5dd7d367)


# Job-portals vs Postings
The summary is written by Copilot.

**Estonia**: The highest number of job postings is on LinkedIn (7). Other portals like Wellfound, Recruit.net, and Startup Jobs have fewer postings. The least number of postings are found on portals such as Ai-Jobs.net, Kandideeri EE, Kandideeri.ee, Placement India, and Trabajo.org(each with 1 posting).

**Finland**: The most job postings are on Trabajo.org(42), followed by LinkedIn Finland (13) and Työpaikat | Indeed (10). Other portals, like SmartRecruiters Job Search, Snowflake Careers, and Technojobs, each have only one posting.

**Latvia**: Both ProZ.comand Recruit.net have only one job posting.

**Lithuania**: The highest number of job postings is on Trabajo.org(8). Other portals mentiond are BeBee, LinkedIn, Sports Tech Jobs, Tech4Good Jobs, aAi-Jobs.neteach.

![Image](https://github.com/user-attachments/assets/8389c2c7-ee4d-4151-be41-fe3d0eeca16b)
```sql
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
```


# Job Postings By Company
Bolt, Wolt, Nortal, Veriff are familiar names in Estonia. Banks, university and state-owned enteprise (Omniva post delivery,logistics) ca be also found.
Top three companies from the list:
	- Hostinger is a web hosting company.
 	- Aspo area is business-developing/shareholding.
  	- Gapgemini offers also business-consult.


![Image](https://github.com/user-attachments/assets/7b44d25e-fd9a-43cd-8a62-95eb7038bbb1)

![Image](https://github.com/user-attachments/assets/4b4c6592-399e-4175-9e47-440dfb284fae)

```sql
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
```

# Top 10 skills 
According to job-titles with word "Analyst" and in Estonia/Latvia/Estoni/Finland top 10 skills are:
![image](https://github.com/user-attachments/assets/b8da5cde-2c93-4a70-8b21-28e02e73a864)

```sql
WITH skills_listing AS (
SELECT  skill_id, count(skill_id) as demand_for_skill 
FROM skills_job_dim AS sjd
INNER JOIN job_postings_fact AS jpf
ON sjd.job_id = jpf.job_id
WHERE jpf.job_title_short LIKE '%Analyst%'
AND job_location IN ('Estonia', 'Lithuania', 'Latvia', 'Finland') 
GROUP BY skill_id
)

SELECT skills_dim.skill_id, skills_dim.skills, skills_listing.demand_for_skill FROM skills_dim
INNER JOIN skills_listing
 ON skills_dim.skill_id = skills_listing.skill_id
ORDER BY skills_listing.demand_for_skill DESC 
LIMIT 10
```

Here is comparing queries results to the world TOP10 skills with job title "Analyst"

![Kuvatõmmis 2025-02-06 154417](https://github.com/user-attachments/assets/64b53ffd-138d-40b8-bb99-6e39d5df9d21)

And Copilot's comparing table:

| **Skill**    | **Position in Estonia, Latvia, Lithuania, and Finland** | **Position Globally** |
|--------------|----------------------------------------------------------|-----------------------|
| SQL          | 1st                                                      | 1st                   |
| Python       | 2nd                                                      | 3rd                   |
| Tableau      | 3rd                                                      | 4th                   |
| Excel        | 4th                                                      | 2nd                   |
| Power BI     | 5th                                                      | 5th                   |
| R            | 6th                                                      | 6th                   |
| Azure        | 7th                                                      | -                     |
| Looker       | 8th                                                      | -                     |
| AWS          | 9th                                                      | -                     |
| Go           | 10th                                                     | -                     |
| PowerPoint   | -                                                        | 7th                   |
| Word         | -                                                        | 8th                   |
| SAS          | -                                                        | 9th                   |



-- avg_salary, job_title doesn't matter
-- avg_salary
```sql
SELECT job_title_short,
job_location,
salary_year_avg,
round(salary_year_avg/12) as paid_monthly,
name as company
FROM job_postings_fact
LEFT JOIN company_dim
ON company_dim.company_id = job_postings_fact.company_id
WHERE 
job_location IN ('Estonia', 'Lithuania', 'Latvia', 'Finland') 
AND salary_year_avg IS NOT NULL
ORDER BY salary_year_avg DESC
```
![Kuvatõmmis 2025-02-04 102953](https://github.com/user-attachments/assets/f49f635c-c729-4f64-8dbf-9953d2dd173d)


// siia vahele
```sql
SELECT job_title_short, job_id,
job_location,
salary_year_avg,
round(salary_year_avg/12) as paid_monthly,
name as company
FROM job_postings_fact
LEFT JOIN company_dim
ON company_dim.company_id = job_postings_fact.company_id
WHERE 
job_location IN ('Estonia', 'Lithuania', 'Latvia', 'Finland') 
AND salary_year_avg IS NOT NULL
AND job_title_short LIKE '%Analyst%'
ORDER BY salary_year_avg DESC
```
![Kuvatõmmis 2025-02-04 113606](https://github.com/user-attachments/assets/4e9dbac5-b50c-41c3-9c29-7521ab39b3e5)

-- avr_salary and skills

-- avg_salary
```sql
WITH 
    skills_listing AS ( SELECT skill_id, count(skill_id) as demand_for_skill
     FROM skills_job_dim AS sjd INNER JOIN job_postings_fact AS jpf ON sjd.job_id = jpf.job_id 
    WHERE jpf.job_title_short LIKE '%Analyst%' AND job_location IN ('Estonia', 'Lithuania', 'Latvia', 'Finland') AND jpf.salary_year_avg IS NOT NULL
    GROUP BY skill_id )

SELECT skills_dim.skill_id, skills_dim.skills, skills_listing.demand_for_skill FROM skills_dim INNER JOIN skills_listing ON skills_dim.skill_id = skills_listing.skill_id ORDER BY skills_listing
```
![Kuvatõmmis 2025-02-04 113431](https://github.com/user-attachments/assets/35d38b08-f1d4-422a-a495-c756f02da334)
