## 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT `students`.*, `degrees`.`name`
FROM `students`
INNER JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = "corso di laurea in economia";

## 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT * 
FROM `degrees`
LEFT JOIN `departments` ON `department_id` = `degrees`.`id`
WHERE `departments`.`name` = "dipartimento di neuroscienze"
AND `degrees`.`name` LIKE "%corso di laurea magistrale%";

## 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT `courses`.*
FROM `course_teacher`
INNER JOIN `teachers` ON `teacher_id` = `teachers`.`id`
INNER JOIN `courses` ON `course_id` = `courses`.`id`
WHERE `teachers`.`id` = 44;

## 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT * 
FROM `students`
INNER JOIN `degrees` ON `degree_id` = `degrees`.`id`
INNER JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name`;

## 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
## 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
## 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.