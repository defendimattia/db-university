## 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```
SELECT CONCAT(`students`.`name`, " ", `students`.`surname`) AS `fullname`, `degrees`.`name`
FROM `students`
INNER JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = "corso di laurea in economia";
```

## 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```
SELECT * 
FROM `degrees`
LEFT JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = "dipartimento di neuroscienze"
AND `degrees`.`level` = "magistrale";
```

## 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```
SELECT `courses`.*, CONCAT(`teachers`.`name`, " ", `teachers`.`surname`) AS `teacher_fullname`
FROM `course_teacher`
INNER JOIN `teachers` ON `teacher_id` = `teachers`.`id`
INNER JOIN `courses` ON `course_id` = `courses`.`id`
WHERE `teachers`.`id` = 44;
```

## 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```
SELECT `students`.`name`, `students`.`surname`, `degrees`.`name`, `departments`.`name`
FROM `students`
INNER JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
INNER JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name`;
```

## 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```
SELECT `degrees`.`name` AS `degree_name`, `courses`.`name` AS `course_name`, CONCAT(`teachers`.`name`, " ", `teachers`.`surname`) AS `teacher_fullname`
FROM `course_teacher`
INNER JOIN `courses` ON `course_id` = `courses`.`id`
INNER JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
INNER JOIN `teachers` ON `teacher_id` = `teachers`.`id`;
```

## 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```
SELECT DISTINCT `teachers`.*, `departments`.`name`
FROM `course_teacher`
INNER JOIN `courses` ON `course_id` = `courses`.`id`
INNER JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
INNER JOIN `teachers` ON `teacher_id` = `teachers`.`id`
INNER JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = "dipartimento di matematica";
```

## 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

```
SELECT `student_id`, COUNT(`exam_id`) AS `num_exams`, MAX(`vote`) AS `max_vote`, COUNT(CASE WHEN `vote` >= 18 THEN 1 END) AS `min_18`
FROM `exam_student`
GROUP BY (`student_id`);
```