Group by:
1. Contare quanti iscritti ci sono stati ogni anno

SELECT COUNT(`id`) AS `enroled_student_for_year`, YEAR(`enrolment_date`) FROM `students` GROUP BY YEAR(`enrolment_date`);

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT COUNT(`id`) AS `number_teachers`, `office_number` FROM `teachers` GROUP BY `office_number`;

3. Calcolare la media dei voti di ogni appello d'esame

SELECT ROUND(AVG(`vote`),2) AS `average_vote` FROM `exam_student`;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT COUNT(`id`) AS `courses_for_department`, `department_id` FROM `degrees` GROUP BY `department_id`;

Joins:
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT * FROM `students` INNER JOIN `degrees` ON degrees.id = students.degree_id WHERE `degrees`.name = "Corso di Laurea in Economia";

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT* FROM `degrees` INNER JOIN `departments` ON degrees.department_id = departments.id WHERE degrees.level = "magistrale" AND departments.name = "Dipartimento di Neuroscienze";

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT `courses`.`name`, `teachers`.`name`, `teachers`.`surname`
FROM `courses`
INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
WHERE `teachers`.`name` = "Fulvio" 
AND `teachers`.`surname` = "Amato";

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT `students`.`name`, `students`.`surname`, `departments`.`name`
FROM `students`
INNER JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name` ASC;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

`degrees`.`name` AS `degree_name`,
`courses`.`name` AS `course_name`,
`teachers`.`surname` AS `teacher_name`,
`teachers`.`name` AS `teacher_surname`,

FROM `degrees`
INNER JOIN `courses`
ON `courses`.`degree_id` = `degrees`.`id`
INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT `departments`.`name` AS `department_name`,
`teachers`.`surname` AS `teacher_name`,
`teachers`.`name` AS `teacher_surname`

FROM `teachers`
INNER JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
INNER JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`
INNER JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = "Dipartimento di Matematica";

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.


## NON FUNZIONA
SELECT `students`.`name`, `students`.`surname`, `students`.`id`,
`courses`.`name` AS `course_exam_name`
FROM `students`
INNER JOIN `exam_student`
ON `students`.`id` = `exam_student`.`student_id`
INNER JOIN `exams`
ON `exam_student`.`exam_id` = `exams`.`id`
INNER JOIN `courses`
ON `exams`.`course_id` = `courses`.`id`
COUNT(`students`.`id`)
GROUP BY `students`.`couerse_exam_name`