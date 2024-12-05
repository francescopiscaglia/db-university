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
FROM `exam_student`;

# Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT COUNT(`id`) as `courses_number`, `department_id`
FROM `degrees`
GROUP BY `department_id`;


## Join
# Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT 
  `students`.`id` AS `student_id`,
  `students`.`name` AS `student_name`,
  `students`.`surname` AS `student_surname`,
  `students`.`date_of_birth` AS `student_date_of_birth`,
  `degrees`.`id` AS `degree_id`,
  `degrees`.`name` AS `degree_name`
FROM `degrees`
JOIN `students` ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = "Corso di Laurea in Economia";

# Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
SELECT 
  `departments`.`id` AS `department_id`,
  `departments`.`name` AS `department_name`,
  `degrees`.`id` AS `degree_id`,
  `degrees`.`name` AS `degree_name`,
  `degrees`.`level` AS `degree_level`
FROM `departments`
JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = "Dipartimento di Neuroscienze"
AND `degrees`.`level` = "magistrale";

# Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
SELECT 
  `teachers`.`id` AS `teacher_id`,
  `teachers`.`name` AS `teacher_name`,
  `teachers`.`surname` AS `teacher_surname`,
  `courses`.`id` AS `course_id`,
  `courses`.`name` AS `course_name`,
  `courses`.`description` AS `course_description`
FROM `courses`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`id` = 44;

# Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
SELECT 
  `students`.`id` AS `student_id`, 
  `students`.`name` AS `student_name`, 
  `students`.`surname` AS `student_surname`, 
  `degrees`.`id` AS `degree_id`, 
  `degrees`.`name` AS `degree_name`, 
  `departments`.`id` AS `department_id`, 
  `departments`.`name` AS `department_name`
FROM `departments`
JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id`
JOIN `students` ON `degrees`.`id` = `students`.`degree_id`
ORDER BY `students`.`surname`, `students`.`name`;

# Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
SELECT 
  `degrees`.`id` AS `degrees_id`, 
  `degrees`.`name` AS `degrees_name`, 
  `courses`.`id` AS `course_id`, 
  `courses`.`name` AS `course_name`, 
  `courses`.`description` AS `course_description`, 
  `teachers`.`id` AS `teacher_id`, 
  `teachers`.`name` AS `teacher_name`, 
  `teachers`.`surname` AS `teacher_surname`
FROM `degrees`
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`;

# Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54 row)
SELECT DISTINCT
  `teachers`.`id` AS `teacher_id`,
  `teachers`.`name` AS `teacher_name`,
  `teachers`.`surname` AS `teacher_surname`
FROM `departments`
JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id`
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `departments`.`name` = "Dipartimento di Matematica";

# BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.