# finserve-A-B-test
A simple A/B testing project analysing conversion rates for two customer groups. Includes SQL queries, Excel calculations, and a Power BI dashboard.

# Overview
This project is a self-created A/B test to practice and demonstrate end-to-end skills in:

- Designing an experiment.
- Querying and cleaning data using SQL.
- Performing statistical calculations in Excel.
- Building an interactive dashboard in Power BI.

The goal was to compare two versions of a loan application flow (Group A vs Group B) and measure which one leads to more completed applications.

# How the A/B Test Was Created
Since this was a self-built project, I generated a synthetic dataset using SQL.

The dataset includes:
- 50,000 users
- Assigned into two random groups: A and B
- Device (Desktop / Mobile)
- Region (North / South / East / West)
- Visit date
- Whether the user completed the loan application (0/1)

# How groups were formed
While generating data, each user was randomly assigned to a group:

- Group A → Old version of the loan application page
- Group B → Updated version of the application page
The purpose was to check if the small changes in the design improved conversion.

*This structure simulates how a real A/B test is done in companies.*

# Dataset Structure
Table: ab_test_data

| Column                | Description                      |
| --------------------- | -------------------------------- |
| user_id               | Unique user ID                   |
| group                 | A or B                           |
| region                | User’s region                    |
| device                | Desktop or Mobile                |
| visit_date            | Date of visit                    |
| completed_application | 1 = completed, 0 = not completed |


# SQL Queries Used

```
Fetching total users, conversions, and conversion rate:
SELECT 
    `group`,
    COUNT(*) AS total_users,
    SUM(completed_application) AS conversions,
    ROUND(SUM(completed_application)*100.0 / COUNT(*), 2) AS conversion_rate
FROM ab_test_data
GROUP BY `group`
ORDER BY `group`;
```

# Results (A vs B)

| Metric                 | Group A | Group B |
| ---------------------- | ------- | ------- |
| Users                  | 24,947  | 25,053  |
| Completed Applications | 1,699   | 1,964   |
| Conversion Rate        | 6.81%   | 7.84%   |

*Key Insight*
Group B performed better, with a 1.03% absolute improvement in conversion.

# Statistical Testing
To check if the improvement was real (not random), a z-test for proportions was calculated manually in Excel.

| Statistic                        | Value   |
| -------------------------------- | ------- |
| Pooled Conversion                | 7.33%   |
| Standard Error                   | 0.00233 |
| Z-Score                          | 4.41    |
| P-Value                          | 0.00001 |
| Difference                       | 1.03%   |
| Incremental Conversions          | 265     |
| Extra Conversions per 100k Users | 1030    |

*Interpretation:*
The p-value is extremely low, meaning the improvement is statistically significant.

# Power BI Dashboard
A report was built to visualize:

- Total users
- Total conversions
- Overall conversion rate
- Conversion by group
- Conversions by device and region

*Screenshots of the Power BI dashboard are included in the repository.*

# Project Takeaways
This project demonstrates:

- How to design and structure an A/B test.
- How to query experiment data in SQL.
- How to calculate statistical significance manually.
- How to convert raw data into insights.
- How to present findings visually using Power BI.
- The project follows the typical workflow used in product, analytics, and growth teams.

# Conclusion
The A/B test shows a clear difference between the two variants.
While both groups had a similar number of users, Group B consistently outperformed Group A in completed loan applications.

- Group B’s conversion rate was 7.84%, compared to 6.81% for Group A.
- The improvement of 1.03% may look small, but at this scale it resulted in 265 additional conversions in the sample.
- Statistical testing confirmed that the lift is significant, meaning the results are unlikely to be due to random variation.

If this were a real experiment, the practical recommendation would be to roll out version B to all users, as it shows a measurable and statistically reliable improvement.


