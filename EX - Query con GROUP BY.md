SOLUTIONS

```sql

1. Contare quanti iscritti ci sono stati ogni anno?

SELECT YEAR(`enrolment_date`) AS anno, COUNT(*) AS num_studenti
FROM `students`
GROUP BY YEAR(`enrolment_date`)
ORDER BY anno ASC
#corretto mettere `id` in COUNT() rispetto a *

2. Contare gli insegnanti che hanno l"'"ufficio nello stesso edificio?

SELECT `office_address` AS ufficio_indirizzo, COUNT(*) AS tot_insegnanti_stesso_ufficio
FROM `teachers`
GROUP BY `office_address`
#corretto mettere `id` in COUNT() rispetto a *

3. Calcolare la media dei voti di ogni appello d"'"esame? Non sicuro

SELECT `vote`, AVG(`vote`)
FROM `exam_student`
GROUP BY `vote`

#soluzione corretta
SELECT `exam_id`, AVG(`vote`)
FROM `exam_student`
GROUP BY `exam_id`

4. Contare quanti corsi di laurea ci sono per ogni dipartimento?

SELECT `name`, COUNT(`name`)
FROM `departments`
GROUP BY `name`

#soluzione_corretta
SELECT `department_id`, COUNT(`id`)
FROM `degrees`
GROUP BY `department_id`


```
