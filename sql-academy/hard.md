# Решения бесплатных задач тяжелого уровня с сайта sql-academy 

*44. Найдите максимальный возраст (количество лет) среди обучающихся 10 классов на сегодняшний день. Для получения текущих даты и времени используйте функцию NOW(). ([ссылка](https://sql-academy.org/ru/trainer/tasks/44))*

<details>
<summary>Решение</summary>

``` sql
SELECT max(TIMESTAMPDIFF(year, birthday, NOW())) AS max_year
FROM Student s
	JOIN Student_in_class sic ON s.id = sic.student
	JOIN Class c ON sic.class = c.id
WHERE c.name LIKE '%10%'
```
</details>
