Different operations + practice 3 from the series.

```sql
-- drop hours_rate - 5
-- raise hours rate + 5

SELECT 
    project_company, 
    nerd_id, 
    nerd_role, 
    hours_rate AS original_rate,
    hours_rate-5 AS drop_rate,
    hours_rate + 5 AS hike_rate
FROM invoices_fact
LIMIT 5;
```


![Image](https://github.com/user-attachments/assets/425d7b74-13b5-422c-aa03-dfdaf1406d65)





```sql
-- projects which only cost more than 100 after hike_rate = hike_rate * hours_spent
SELECT 
    project_company, 
    nerd_role,
    hours_spent,
    hours_rate,
    hours_rate AS original_rate,
    hours_rate +5 AS hike_rate,
-- just for control 
	(hours_rate +5)*hours_spent as project_total
FROM invoices_fact
-- origin
	-- WHERE hike_rate * hours_spent > 1000
WHERE project_total > 1000
LIMIT 5;
```

![image](https://github.com/user-attachments/assets/f1baf15e-ccc2-4583-9f14-8d0a7f2ca69b)







```sql
--Modulus % e.g working overhours
-- returning that is left

SELECT
    activity_id,
    hours_spent,
    hours_spent % 8 as extra_hours
FROM invoices_fact
WHERE
	(hours_spent BETWEEN 8 AND 16) AND extra_hours > 0 
ORDER BY hours_spent DESC
LIMIT 5;

```

![Image](https://github.com/user-attachments/assets/f41ebb5b-2a51-474b-9144-5e0b8ffc1911)



```sql
-- CALCULATE total by project

SELECT 
project_id, 
    hours_spent,
    hours_rate AS original_rate,
    SUM (hours_rate * hours_spent) AS total_project,
    SUM (hours_rate * hours_spent) AS estamate_total_project
FROM invoices_fact
GROUP BY project_id
LIMIT 5;

```

![image](https://github.com/user-attachments/assets/c67f71d8-e6bb-4ef7-bf54-354eb715b735)
