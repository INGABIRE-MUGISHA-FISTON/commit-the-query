PL/SQL ASSIGNMENT

 INGABIRE MUGISHA FISTON 27217  
 MUYOBOKE EMMANUEL  26227
GROUP B  



 Overview
This project contains PL/SQL queries and analysis using window functions . The dataset provides information such as MP ID, name, district, gender, political party, appointment date, and monthly salary. Our aim is to use SQL window functions to gain meaningful insights from the dataset.

 Objectives
- Apply SQL window functions on real-world data.  
- Use analytical functions like LAG(), LEAD(), RANK(), DENSE_RANK(), and ROW_NUMBER() effectively.  
- Perform complex queries to extract insights from the dataset.  
- Demonstrate real-life use cases of SQL window functions.  
- Document the SQL process clearly and professionally.

 Dataset Structure
The dataset consists of the following columns:
- mp_id: Unique identifier of the MP
- full_name: Full name of the MP
- district: District the MP represents
- gender: Gender of the MP
- party: Political party
- appointment_date: Date of appointment
- monthly_salary: MP's monthly salary

Step 1: User Creation
sql
CREATE USER auca IDENTIFIED BY 1111;
GRANT ALL PRIVILEGES TO auca;


 Step 2: Table Creation and Data Insertion
sql
CREATE TABLE rwanda_parliament (
    mp_id NUMBER PRIMARY KEY,
    full_name VARCHAR2(120),
    district VARCHAR2(50),
    gender VARCHAR2(10),
    party VARCHAR2(50),
    appointment_date DATE,
    monthly_salary NUMBER
);

(Sample data inserted for analysis)

 Analysis Queries

 1. First 2 MPs Appointed Per District
Using ROW_NUMBER() to find the first two MPs per district based on appointment date.

 2. Rank MPs by Salary Within Each District
Using RANK() and DENSE_RANK() to classify MPs' salaries within districts.

 3. Top 3 Salaries Per Party
sql
SELECT * FROM (
    SELECT *, RANK() OVER (PARTITION BY party ORDER BY monthly_salary DESC) AS salary_rank
    FROM rwanda_parliament
) WHERE salary_rank <= 3;


 4. Comparison of Salaries Using LAG() and LEAD()
We use these functions to compare each MP's salary with the previous and next MP.
sql
SELECT
    full_name,
    monthly_salary,
    LAG(monthly_salary) OVER (ORDER BY monthly_salary) AS prev_salary,
    LEAD(monthly_salary) OVER (ORDER BY monthly_salary) AS next_salary
FROM rwanda_parliament;


5. Aggregation With Window Functions
Using AVG(), SUM(), etc., as window functions to calculate statistics across all MPs or within groups.

 Conclusion
This PL/SQL assignment demonstrates the importance of window functions in advanced data analysis. By analyzing the Rwandan Parliament dataset, we gained insights into MP appointments, salary distributions, and political party trends. This skill is essential for database professionals working on performance, ranking, and trend analysis.commit-the-query
