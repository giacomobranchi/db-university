# Group by:
1. Contare quanti iscritti ci sono stati ogni anno

```sql

SELECT COUNT(*) 
AS `student_count`, YEAR(`enrolment_date`) 
FROM `students` 
GROUP BY YEAR(`enrolment_date`);

```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql

SELECT COUNT(*) 
AS `teacher_office`, `office_address` 
FROM `teachers` 
GROUP BY `office_address`;

```

3. Calcolare la media dei voti di ogni appello d'esame

```sql

SELECT COUNT(`exam_id`) 
AS `average`, AVG(`vote`) 
FROM `exam_student` 
GROUP BY `exam_id`;

```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql

SELECT COUNT(*) 
AS `course_department`, `degree_id` 
FROM `courses` 
GROUP BY `degree_id`;

```


# Joins:
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql

SELECT * FROM `students` 
INNER JOIN `degrees` 
ON `degrees`.`id` = `students`.`degree_id` 
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql

    SELECT * FROM `degrees` 
    INNER JOIN `departments` 
    ON `departments`.`id` = `degrees`.`department_id`
    WHERE `departments`.`name` = 'Dipartimento di Neuroscienze' 
    AND `degrees`.`level` = 'magistrale';

```

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql

SELECT * FROM `courses` 
INNER JOIN `course_teacher` 
ON `course_teacher`.`course_id` = `courses`.`id` 
WHERE `course_teacher`.`teacher_id` = 44;

```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql

SELECT * FROM `students` 
LEFT JOIN `degrees` 
ON `degrees`.`id` = `students`.`degree_id`
LEFT JOIN `departments` 
ON `departments`.`id` = `degrees`.`department_id` 
ORDER BY `surname`, `students`.`name`;

```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql

SELECT * FROM `degrees` 
LEFT JOIN `courses` 
ON `degrees`.`id` = `courses`.`degree_id` 
LEFT JOIN `course_teacher` 
ON `courses`.`id` = `course_teacher`.`course_id` 
LEFT JOIN `teachers` 
ON `teachers`.`id` = `course_teacher`.`teacher_id`;


```


6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql

SELECT `teachers`.`name`, `teachers`.`surname`, `departments`.`name` FROM `teachers` 
LEFT JOIN `course_teacher` 
ON `teachers`.`id` = `course_teacher`.`teacher_id` 
LEFT JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id` 
LEFT JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id` 
LEFT JOIN `departments` ON `departments`.`id` = `degrees`.`department_id` 
WHERE `departments`.`name` = 'Dipartimento di Matematica';


```


# BONUS: 
Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
