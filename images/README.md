# Introduction
This project researches top-paying careers, 
in-demand skills, and where high demand meets high salary in data analytics.

Here are the SQL queries build for the project.
[SQL Project Folder](/project_sql/)
# Background
The data used for this project was gathered from [Luke Barousse's SQL course](https://www.lukebarousse.com/sql).  It includes information on job titles, salaries, locations, and essential skills.

### The questions I wanted to answer through the SQL queries were:
1. What are the top-paying data analyst jobs?
2. What skills are most in demand for data analysis?

# Tools Used
For this project, I utilized numerous tools below:
- **SQL**:  The majority of this project was to show   the SQL queries created to dig into the insights.
- **PostgreSQL**: The selected database management system, to handle the project's data.
- **Visual Studio Code**: My prefered code editor for the variety of projects.
- **Tableau**: Utilized to express insights about the data in a visual manner.
- **Git & GitHub**: Essential for version control and sharing project files and analysis.
# Analysis
Each query for this project aimed at investigating specific aspects of the data analyst job market.
Here is how I approched each question:
### 1. What are the top-paying data analyst jobs?
To identify the highest-paying jobs, I filtered data analyst positionsby average yearly salary and location, with the focus on remote jobs.  The query highlights the high paying opportunities in the field.
```sql
SELECT
    job_id,
    job_title,
    job_location,
    job_schedule_type,
    salary_year_avg,
    job_posted_date,
    name AS company_name 
FROM 
    job_postings_fact
LEFT JOIN company_dim
ON job_postings_fact.company_id = company_dim.company_id
WHERE
    job_title_short = 'Data Analyst' AND
    job_location = 'Anywhere' AND
    salary_year_avg IS NOT NULL
ORDER BY salary_year_avg DESC
LIMIT 10
```
Here's the break down for the top data analyst jobs in 2023:
- **Wide Salary Range:** Top 10 paying data analyst roles span from $184,000 to $650,000, indicating significant salary potiential in the field.
- **Diverse Employers:** Companies like AT&T, Meta, SmartAsset are among those offering high salaries, showing broad interest across different industries.
 - **Job Title Variety:** There is a high diversity in job titles, from Data Analyst to Director of Analytics, reflecting varied roles and specializations within data analytics.
 
![Top Paying Roles](1_top_paying_jobs.png)

*Bar graph visualizing the salary for the top 10 salaries for remote data analysts.
### 2. What skills are most in demand for data analysis?

```sql
SELECT
    skills,
    count(skills_job_dim.job_id) AS demand_count
FROM job_postings_fact
INNER JOIN skills_job_dim
ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim
ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE job_title_short = 'Data Analyst' AND
    job_work_from_home = TRUE
GROUP BY
    skills
ORDER BY
    demand_count DESC
LIMIT 5;
```
Here's the break down for the top in demand skills for data analysts:
- **Structured:** SQL is a highly prized skill for data analysts at being metioned 7291 times.  Excel and Python come in second place at over 4000 mentions each.  Visualization tools such as Tableau and Power BI, which make the insights understandable, round out the top five.

![Top Skills In Demand](3_top_skills_in_demand.png)
*Pie chart visualizing the top 5 in demand skills for remote data analysts.

# Learnings
Throughout this initial project, I've dusted off a lot of SQL skills while adding new items to my data analyst toolbelt.
- **Query Building:** Brushing up on basic SQL structure with SELECT and WHERE statements in order filter the data to find these insights.
- **Data Aggregation:** Jumped into some JOIN and ORDER BY statements to ensure all bits of information are gathered to provide a total view.
# Conclusions
### Insights
1. **Top-Paying Data Analyst Roles:** The highest paying jobs for data analysts that allow remote work offer a wide range of salaries, the highest being $650,000.
2. **In Demand Skills:** Proficientcy in SQL, Excel, Python, Tableau, and Power BI are the most mentioned skills for the variety of data analytic roles.
