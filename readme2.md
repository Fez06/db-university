1. Contare quanti iscritti ci sono stati ogni anno

SELECT YEAR(`enrolment_date`) AS `Annata`, COUNT('id') AS `Iscritti`
FROM `students` 
GROUP BY YEAR(`enrolment_date`)

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT `office_address`, COUNT(`id`)
FROM `teachers` 
GROUP BY `office_address`

3. Calcolare la media dei voti di ogni appello d'esame

SELECT `exam_id`, AVG(`vote`)
FROM `exam_student`
GROUP BY `exam_id`

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT COUNT(`name`), `department_id` 
FROM `degrees` 
GROUP BY `department_id`


<!-- -------------------------------------- -->

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT * 
FROM `students`
JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name`= 'Corso di Laurea in Economia';

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT *
FROM `departments` 
JOIN `degrees` ON `degrees`.`department_id`=`departments`.`id`
WHERE `degrees`.`level`= 'Magistrale' AND `departments`.`name`= 'Dipartimento di Neuroscienze';

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT * 
FROM `teachers` 
JOIN `course_teacher` ON `teachers`.`id`=`course_teacher`.`teacher_id`
WHERE `teachers`.`id`= 44

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il
relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT * 
FROM `students`
JOIN `degrees` ON `students`.`degree_id`= `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id`= `departments`.`id`
ORDER BY `students`.`surname` ASC

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT * 
FROM `degrees`
JOIN `courses` ON `courses`.`degree_id`= `degrees`.`id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id`= `teachers`.`id`

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT DISTINCT `teachers`.`name`, `teachers`.`surname`, `departments`.`name`
FROM `departments` 
JOIN `degrees` ON `degrees`.`department_id`=`departments`.`id`
JOIN `courses` ON `courses`.`degree_id`= `degrees`.`id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id`= `teachers`.`id`
WHERE `departments`.`name`= 'Dipartimento di Matematica';

7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per
superare ciascuno dei suoi esami

