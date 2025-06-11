NEW EXERCISE.
Esercizio di oggi: DB University
nome repo: db-university
Dopo aver importato lo schema allegato in un nuovo DB dentro MySQL Workbench, eseguite le query del file allegato.
Dopo aver testato le vostre query con MySQL Workbench, riportatele in un file di markdown e caricatelo nella vostra repo.
BONUS:
Risolvere anche le query del file GROUP BY e caricarle le soluzioni in un nuovo file di markdown

SOLUTIONS

```sql

1. Selezionare tutti gli studenti nati nel 1990 (160), ok

SELECT  *
FROM `students`
WHERE YEAR(`date_of_birth`) = 1990

2. Selezionare tutti i corsi che valgono più di 10 crediti (479) ok

SELECT *
FROM `courses`
WHERE `cfu` > 10

3. Selezionare tutti gli studenti che hanno più di 30 anni, (1000)

SELECT *
FROM `students`
WHERE YEAR(NOW()) - YEAR(`date_of_birth`) >= 30


4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
   laurea (286) ok

SELECT *
FROM `courses`
WHERE `period` = "I semestre" AND `year` = 1

5. Selezionare tutti gli appelli d"'"esame che avvengono nel pomeriggio (dopo le 14) del"'"
   20/06/2020 (21) ok

SELECT *
FROM `exams`
WHERE `date` = DATE("2020-06-20") and `hour` >"14:00:00"

6. Selezionare tutti i corsi di laurea magistrale (38) ok

SELECT *
FROM `degrees`
WHERE `name` LIKE "%magistrale%"

7. Da quanti dipartimenti è composta l"'"università? (12) ok

SELECT COUNT(`id`)
FROM `departments`

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50) ok

SELECT COUNT(`id`)
FROM `teachers`
WHERE `phone` IS NULL
```
