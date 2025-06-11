SOLUTIONS

```sql

1. Contare quanti iscritti ci sono stati ogni anno?

SELECT YEAR(`enrolment_date`) AS anno, COUNT(*) AS num_studenti
FROM `students`
GROUP BY YEAR(`enrolment_date`)
ORDER BY anno ASC

2. Contare gli insegnanti che hanno l"'"ufficio nello stesso edificio?

SELECT `office_address` AS ufficio_indirizzo, COUNT(*) AS tot_insegnanti-stesso-ufficio
FROM `teachers`
GROUP BY `office_address`

3. Calcolare la media dei voti di ogni appello d"'"esame? Non sicuro

SELECT `vote`, AVG(`vote`)
FROM `exam_student`
GROUP BY `vote`

4. Contare quanti corsi di laurea ci sono per ogni dipartimento?

SELECT `name`, COUNT(`name`)
FROM `departments`
GROUP BY `name`

```
