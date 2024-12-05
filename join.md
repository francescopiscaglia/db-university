## Group by
# Contare quanti iscritti ci sono stati ogni anno
SELECT COUNT(`id`) as `iscritti_per_anno`, YEAR(`enrolment_date`) as `anno di iscrizione`
FROM `students`
GROUP BY YEAR(`enrolment_date`);

# Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT COUNT(`id`) as `teachers`, `office_address`
FROM `teachers`
GROUP BY `office_address`;

# Calcolare la media dei voti di ogni appello d'esame
SELECT AVG(`vote`) as `average`
FROM `exam_student`

# Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT COUNT(`id`) as `courses_number`, `department_id`
FROM `degrees`
GROUP BY `department_id`
