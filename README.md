# Objective
Learn and document all my queries used in the online SQL challenge
---

# Comand: Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.
Query: 
SELECT pt.patient_id, pt.first_name
FROM patients as pt
WHERE first_name like 's%' 
AND first_name LIKE '%s'
AND LENGTH(first_name) >= 6

# Comand: Show first name of patients that start with the letter 'C'
Query: SELECT  pt.first_name
FROM patients as pt
WHERE pt.first_name LIKE 'C%'
