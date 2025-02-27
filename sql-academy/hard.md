# Решения бесплатных задач тяжёлого уровня с сайта sql-academy 

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

*45. Какие кабинеты чаще всего использовались для проведения занятий? Выведите те, которые использовались максимальное количество раз. ([ссылка](https://sql-academy.org/ru/trainer/tasks/45))*

<details>
<summary>Решение</summary>

``` sql
WITH max_stud AS (
	SELECT COUNT(*)
	FROM Schedule
	GROUP BY classroom
	ORDER BY 1 DESC
	LIMIT 1
)
SELECT classroom
FROM Schedule
GROUP BY classroom
HAVING COUNT(*) IN (
		SELECT *
		FROM max_stud
	)
```
</details>


*55. Удалить компании, совершившие наименьшее количество рейсов. ([ссылка](https://sql-academy.org/ru/trainer/tasks/55))*

<details>
<summary>Решение</summary>

``` sql
WITH min_count_fly AS (
	SELECT COUNT(*)
	FROM Company c
		JOIN Trip t ON c.id = t.company
	GROUP BY c.name
	ORDER BY COUNT(*)
	LIMIT 1
) DELETE company
FROM company
	JOIN (
		SELECT c.id
		FROM Company c
			JOIN Trip t ON c.id = t.company
		GROUP BY 1
		HAVING COUNT(*) IN (
				SELECT *
				FROM min_count_fly
			)
	) AS subquery ON company.id = subquery.id;
```
</details>

*58. Добавить отзыв с рейтингом 5 на жилье, находящиеся по адресу "11218, Friel Place, New York", от имени "George Clooney" ([ссылка](https://sql-academy.org/ru/trainer/tasks/58))*

<details>
<summary>Решение</summary>

``` sql
INSERT INTO Reviews (id, reservation_id, rating)
SELECT (
		SELECT COALESCE(MAX(id), 0) + 1
		FROM Reviews
	),
	re.id,
	5
FROM Reservations re
	JOIN Rooms ro ON re.room_id = ro.id
	JOIN Users u ON re.user_id = u.id
WHERE ro.address = '11218, Friel Place, New York'
	AND u.name = 'George Clooney';
```
</details>

*60. Выведите идентификаторы преподавателей, которые хотя бы один раз за всё время преподавали в каждом из одиннадцатых классов. ([ссылка](https://sql-academy.org/ru/trainer/tasks/60))*

<details>
<summary>Решение</summary>

``` sql
SELECT teacher
FROM (
		SELECT DISTINCT teacher,
			name
		FROM Schedule s
			JOIN Class c ON s.class = c.id
		WHERE c.name LIKE '11%'
	) AS sq
GROUP BY 1
HAVING COUNT(*) = 2
```
</details>

*68. Для каждой комнаты, которую снимали как минимум 1 раз, найдите имя человека, снимавшего ее последний раз, и дату, когда он выехал ([ссылка](https://sql-academy.org/ru/trainer/tasks/68))*

<details>
<summary>Решение</summary>

``` sql
SELECT room_id,
	name,
	end_date
FROM Reservations re
	JOIN Users u ON re.user_id = u.id
	JOIN Rooms ro ON re.room_id = ro.id
WHERE end_date IN (
		SELECT max(end_date)
		FROM Reservations re
			JOIN Rooms ro ON re.room_id = ro.id
		GROUP BY room_id
	)
```
</details>

*69. Вывести идентификаторы всех владельцев комнат, что размещены на сервисе бронирования жилья и сумму, которую они заработали ([ссылка](https://sql-academy.org/ru/trainer/tasks/69))*

<details>
<summary>Решение</summary>

``` sql
SELECT u.id AS owner_id,
	sum(IF(re.total IS NULL, 0, re.total)) AS total_earn
FROM Rooms r
	LEFT JOIN Reservations re ON r.id = re.room_id
	JOIN Users u ON u.id = r.owner_id
GROUP BY 1
```
</details>

*71. Найдите какой процент пользователей, зарегистрированных на сервисе бронирования, хоть раз арендовали или сдавали в аренду жилье. Результат округлите до сотых. ([ссылка](https://sql-academy.org/ru/trainer/tasks/71))*

<details>
<summary>Решение</summary>

``` sql
WITH count_users_who_r_and_o AS (
	SELECT COUNT(*)
	FROM (
			SELECT DISTINCT user_id
			FROM Reservations
			UNION
			SELECT DISTINCT owner_id
			FROM Rooms r
				JOIN Reservations re ON r.id = re.room_id
		) AS t
),
count_all_users AS (
	SELECT COUNT(*)
	FROM users
)
SELECT round(
		(
			SELECT *
			FROM count_users_who_r_and_o
		) /(
			SELECT *
			FROM count_all_users
		) * 100,
		2
	) AS percent
```
</details>
