## 1. Selezionare tutti gli studenti nati nel 1990 (160)
SELECT *
FROM `students`
WHERE `date_of_birth` >= '1990-01-01'
AND `date_of_birth` <= '1990-12-31';

## 2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
SELECT *
FROM `courses`
WHERE `cfu` > 10;

## 3. Selezionare tutti gli studenti che hanno più di 30 anni
SELECT *
FROM `students`
WHERE `date_of_birth` > '1994-03-24';

## 4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
SELECT *
FROM `courses`
WHERE `year` = 1
AND `period`= 'I semestre';

## 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
SELECT *
FROM `exams`
WHERE `date`= '2020-06-20'
AND `hour` > '14:00:00';

## 6. Selezionare tutti i corsi di laurea magistrale (38)
SELECT *
FROM `degrees`
WHERE `level`= 'magistrale';

## 7. Da quanti dipartimenti è composta l'università? (12)
SELECT COUNT(`id`)
FROM `departments`;

## 8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
SELECT COUNT(*)
FROM `teachers`
WHERE `phone` IS null;

## 9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo degree_id, inserire un valore casuale)
INSERT INTO `students` (`degree_id`, `name`, `surname`, `date_of_birth`, `fiscal_code`, `enrolment_date`, `registration_number`, `email`)
VALUES (30 , 'Francesco', 'Piscaglia', '2000-09-15', 'PSCFNC00P15H199E', '2024-09-25', '621033', 'piscagliafrancesco@gmail.com');

## 10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126
UPDATE `teachers`
SET `office_number` = 126
WHERE `id` = 58;

## 11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9
DELETE FROM `students`
WHERE `fiscal_code`= 'PSCFNC00P15H199E';
