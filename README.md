# DataScienceCourse4_Assignment3
**Titanic Passengers Advanced Analysis — DS PGC Course 4 Assignment 3**

---

## 📘 Assignment Overview
Analyze the **Titanic passengers** dataset using advanced MySQL features (CTEs, window functions, views, stored procedures) to answer business questions about survival, fares, and passenger ordering. Deliverable: SQL script or Word/PDF with queries, outputs, and explanations.

---

## 🧩 Tasks Summary
1. Find the name and age of the oldest passenger who survived.  
2. Create a view showing passenger survival status, class, age, and fare.  
3. Create a stored procedure to retrieve passengers for a given age range.  
4. Categorize passengers by fare: `Low`, `Medium`, `High`.  
5. Show each passenger’s fare and the fare of the **next** passenger (LEAD).  
6. Show each passenger’s age and the **previous** passenger’s age (LAG).  
7. Rank passengers by fare (RANK).  
8. Rank passengers by fare without gaps (DENSE_RANK).  
9. Assign row numbers ordered by fare (ROW_NUMBER).  
10. Use a CTE to compute average fare and list passengers who paid above average.

---

## 🧰 Tools & Techniques (copy-paste-ready code examples)
```sql
-- Oldest surviving passenger (example)
SELECT first_name, last_name, age
FROM titanic
WHERE age = (
  SELECT MAX(age) FROM titanic WHERE survived = 1
) AND survived = 1;

-- Example view
CREATE VIEW Survived_View AS
SELECT survived AS survival_status, pclass, age, fare
FROM titanic;

-- Stored procedure (example)
DELIMITER $$
CREATE PROCEDURE GetPassengersByAge(IN min_age INT, IN max_age INT)
BEGIN
  SELECT * FROM titanic WHERE age BETWEEN min_age AND max_age;
END $$
DELIMITER ;

-- Example window function (next fare)
SELECT passenger_no, first_name, last_name, fare,
  LEAD(fare) OVER (ORDER BY fare) AS next_passenger_fare
FROM titanic;

-- CTE to find passengers above average fare
WITH AvgFare AS (
  SELECT AVG(fare) AS avg_fare FROM titanic
)
SELECT passenger_no, first_name, last_name, fare
FROM titanic
WHERE fare > (SELECT avg_fare FROM AvgFare);
```

---

## 📂 Files included
- `DataScienceCourse4Assignment3Question.pdf` — assignment brief.  
- `DataScienceCourse4Assignment3Solution.pdf` — SQL solution with queries and outputs.

---

## 🧭 How to review
1. Download the solution PDF.  
2. Copy the SQL queries into your MySQL client (MySQL Workbench / DBeaver).  
3. Run each query and compare results to the PDF outputs.  
4. For stored procedures/views, create them in the database and test with sample parameters.

---

## 👤 Author
**Utkarsh Anand** — DS PGC Course 4
