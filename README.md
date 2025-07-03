# Objective
Learn and document all my queries used in the online SQL challenge


## Command: Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.
Query: 
SELECT pt.patient_id, pt.first_name
FROM patients as pt
WHERE first_name like 's%' 
AND first_name LIKE '%s'
AND LENGTH(first_name) >= 6

## Command: Show first name of patients that start with the letter 'C'
Query: SELECT  pt.first_name
FROM patients as pt
WHERE pt.first_name LIKE 'C%'

## Command: Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date. 
SELECT first_name, last_name, birth_date
FROM patients
where birth_date LIKE '197%'
order by birth_date ASC

## Command: Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)
SELECT first_name, last_name
FROM patients
where weight between 100 AND 120

## Command: Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'
UPDATE patients
SET allergies = 'NKA'
WHERE allergies is NULL

## Command: Show patient_id, first_name, last_name from patients whose does not have any records in the admissions table. (Their patient_id does not exist in any admissions.patient_id rows.)
SELECT patients.patient_id, first_name, last_name
FROM patients 
LEFT JOIN admissions 
on patients.patient_id = admissions.patient_id
WHERE admissions.patient_id is NULL

## Command: Show all of the patients grouped into weight groups. Show the total amount of patients in each weight group. Order the list by the weight group descending. For example, if they weight 100 to 109 they are placed in the 100 weight group, 110-119 = 110 weight group, etc.
SELECT count(first_name) as patients_in_group,
FLOOR(weight / 10) * 10 as weight_group
FROM patients
GROUP BY weight_group
order by weight_group desc

