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

## Command: Show patient_id, weight, height, isObese from the patients table. Display isObese as a boolean 0 or 1. Obese is defined as weight(kg)/(height(m)2) >= 30. weight is in units kg. height is in units cm.
SELECT patient_id,
weight,
height,
case 
when weight/Power(height / 100.0, 2) >= 30 THEN 1
Else 0
END as is_obese
FROM patients

## Command: Show the total amount of male patients and the total amount of female patients in the patients table. Display the two results in the same row.
SELECT 
COUNT(CASE WHEN gender = 'M' THEN 1 END) AS male_count,
COUNT(CASE WHEN gender = 'F' THEN 1 END) AS female_count
FROM patients

## Command: We are looking for a specific patient. Pull all columns for the patient who matches the following criteria: - First_name contains an 'r' after the first two letters. - Identifies their gender as 'F' - Born in February, May, or December - Their weight would be between 60kg and 80kg - Their patient_id is an odd number - They are from the city 'Kingston'
SELECT *,
month(birth_date) as mbd
FROM patients
WHERE first_name Like '__%r%'
AND gender = 'F'
AND weight >= 60 and  weight <= 80
AND patient_id % 2 = 1
AND (mbd = 2 OR mbd = 3 OR mbd = 12)
AND city = 'Kingston'
