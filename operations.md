Different operations + practice 3 from the series.

```sql
SELECT 
	project_company, 
    nerd_id, 
    nerd_role, 
    hours_rate AS original_rate,
    hours_rate-5 AS drop_rate,
    hours_rate + 5 AS hike_rate
FROM invoices_fact;
```



```sql
-- projects which only cost more than 100 after hike_rate = hike_rate * hours_spent
SELECT 
	project_company, 
    nerd_id, 
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
WHERE project_total > 1000;
```



```sql
-- % e.g working overhours
-- returning that is left
SELECT
	activity_id,
    hours_spent,
    hours_spent % 8 as extra_hours
FROM invoices_fact
WHERE
	(hours_spent BETWEEN 8 AND 16) AND extra_hours > 0 
ORDER BY hours_spent DESC;

```
