1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
   Neuroscienze
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
   sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
   nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,
   filtrare i tentativi con voto minimo 18.

SOLUZIONI:

### 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia (1000 trovato)

```sql
SELECT *

FROM `students`

INNER JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`

WHERE `degrees`.`name` = "Corso di Laurea in Economia"
```

### 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di

Neuroscienze (1 riga)

```sql

SELECT *
FROM `departments`
INNER JOIN `degrees`
ON `departments`.`id` = `degrees`.`id`
WHERE (`degrees`.`level` = "magistrale") AND
(`departments`.`name`= "Dipartimento di Neuroscienze")
```

### 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44) (11 righe)

```sql

SELECT *

FROM `teachers`

INNER JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`

INNER JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`

WHERE `teachers`.`id` = 44
```

### 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui

sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome

```sql

   SELECT *
FROM `students`

INNER JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`

INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`

ORDER BY `students`.`surname` AND `students`.`name` ASC
```

### 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
SELECT *
FROM `degrees`
INNER JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers`
ON `course_teacher`.`teacher_id`= `teachers`.`id
```

### 6. Selezionare tutti i docenti che insegnano nel Dipartimento di

Matematica (54)

```sql
SELECT
`teachers`.`id`,
`teachers`.`name`,
`teachers`.`surname`,
`teachers`.`phone`,
`teachers`.`email`,
`teachers`.`office_address`,
`teachers`.`office_number`,
`departments`.`name`
FROM `teachers`
INNER JOIN `course_teacher`
ON `course_teacher`.`teacher_id`= `teachers`.`id`
INNER JOIN `courses`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `degrees`
ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN  `departments`
ON `degrees`.`department_id`= `departments`.`id`
WHERE `departments`.`name` = "Dipartimento di Matematica"
GROUP BY `teachers`.`id`,`departments`.`name`
ORDER BY `teachers`.`id`
```

### SOLUZIONE MIGLIORE

```sql

SELECT DISTINCT
`teachers`.`id`,
`teachers`.`name`,
`teachers`.`surname`,
`teachers`.`phone`,
`teachers`.`email`,
`teachers`.`office_address`,
`teachers`.`office_number`,
`departments`.`name`
FROM `teachers`
INNER JOIN `course_teacher`
ON `course_teacher`.`teacher_id`= `teachers`.`id`
INNER JOIN `courses`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `degrees`
ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN  `departments`
ON `degrees`.`department_id`= `departments`.`id`
WHERE `departments`.`name` = "Dipartimento di Matematica"

```

### 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti

per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.

```sql

SELECT
 `students`.`id`,
 `students`.`name`,
 `courses`.`id`,
 `courses`.`name`,
 COUNT(*) AS count_student_of_exam,
 MAX(`exam_student`.`vote`) AS max_vote
FROM `students`
 INNER JOIN `exam_student`
  ON `students`.`id` = `exam_student`.`student_id`
 INNER JOIN `exams`
  ON `exam_student`.`exam_id`=`exams`.`id`
 INNER JOIN `courses`
  ON `exams`.`course_id`= `courses`.`id`
GROUP BY `students`.`id`, `courses`.`id`
HAVING max_vote > 18
ORDER BY `students`.`id`

```

### SOLUZIONI CORRETTA

```sql

SELECT
 `students`.`id`,
 `students`.`name`,
 `courses`.`id`,
 `courses`.`name`,
 COUNT(*) AS count_student_of_exam,
 MAX(`exam_student`.`vote`) AS max_vote
FROM `students`
 INNER JOIN `exam_student`
  ON `students`.`id` = `exam_student`.`student_id`
 INNER JOIN `exams`
  ON `exam_student`.`exam_id`=`exams`.`id`
 INNER JOIN `courses`
  ON `exams`.`course_id`= `courses`.`id`
GROUP BY `students`.`id`, `courses`.`id`
HAVING max_vote >= 18
ORDER BY `students`.`id`

```
