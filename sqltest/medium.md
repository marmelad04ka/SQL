# Решения бесплатных задач среднего уровня с сайта sqltest

*1. Найдите всех клиентов магазина с id 2 (store_id = 2). ([ссылка](https://sqltest.online/ru/question/normal/find-customers-full-names))*

<details>
<summary>Решение</summary>

``` sql
select concat( first_name , ' ',  last_name ) as full_name,  email 
from customer
where store_id = 2
order by  last_name 
```
</details>


*2. Напишите запрос, который возвращает адреса и почтовые индексы всех адресов, расположенных в London. ([ссылка](https://sqltest.online/ru/question/normal/find-addresses-using-sub-query))*

<details>
<summary>Решение</summary>

``` sql
select  address , postal_code 
from address
where city_id in (select city_id from city where city = 'London')
```
</details>

*3. Напишите запрос, который возвращает адреса и почтовые индексы всех адресов, расположенных в London, с помощью JOIN. ([ссылка](https://sqltest.online/ru/question/normal/find-addresses-using-join)*

<details>
<summary>Решение</summary>

``` sql
select  address , postal_code 
from address
 join city using(city_id)
where city = "London"
```
</details>

*4. Найдите все имена встречающиеся более одного раза. ([ссылка](https://sqltest.online/ru/question/normal/find-duplicate-actor-names)*

<details>
<summary>Решение</summary>

``` sql
select  first_name , count(*) as count
from actor
group by 1
having count(*) > 1
```
</details>

*5. Найдите самую популярную среди актеров фамилию.  ([ссылка](https://sqltest.online/ru/question/normal/find-the-most-popular-surname-among-actors))*

<details>
<summary>Решение</summary>

``` sql
select last_name, count(*) as count
from actor
group by last_name
order by count desc
limit 1
```
</details>

*6. Найдите всех актёров снимавшихся в фильме ANGELS LIFE.  ([ссылка](https://sqltest.online/ru/question/normal/find-all-the-actors-in-the-film))*

<details>
<summary>Решение</summary>

``` sql
select  first_name , last_name 
from actor
 join film_actor using(actor_id)
 join film f using(film_id)
where f.title = 'ANGELS LIFE'
group by actor_id
order by 2
```
</details>

*7. Найдите все фильмы в которых снимался HENRY BERRY.  ([ссылка](https://sqltest.online/ru/question/normal/find-all-films-of-an-actor))*

<details>
<summary>Решение</summary>

``` sql
with st as (select film_id
from film_actor
join actor on film_actor.actor_id = actor.actor_id and first_name = 'HENRY' and last_name = 'BERRY')
select  title , release_year , rating
from film
where film_id in (select * from st)
order by 3
```
</details>

*8. Подсчитайте количество фильмов относящихся к каждой из категорий.   ([ссылка](https://sqltest.online/ru/question/normal/find-the-distribution-of-films-by-category))*

<details>
<summary>Решение</summary>

``` sql
select name as category, count(*) as count
from category
join film_category using(category_id)
group by 1
order by 2 desc
```
</details>

*9. Найдите среднюю продолжительность фильма для каждой категории.   ([ссылка](https://sqltest.online/ru/question/normal/average-length-of-a-movie-by-category))*

<details>
<summary>Решение</summary>

``` sql
select c.name as category, avg(f.length) as avg_film_length
from category c
 join film_category fc using(category_id)
 join film f using(film_id)
group by category_id
order by 1
```
</details>

*10. Найдите количество фильмов в которых принимал участие HENRY BERRY   ([ссылка](https://sqltest.online/ru/question/normal/find-the-number-of-films-in-which-the-actor-took-part))*

<details>
<summary>Решение</summary>

``` sql
select count(*) as film_count
from film_actor fa
 join actor a on fa.actor_id = a.actor_id and first_name = 'HENRY' and last_name = 'BERRY'
```
</details>

*11. Найдите актёров более популярных чем HENRY BERRY  ([ссылка](https://sqltest.online/ru/question/normal/find-actors-more-popular-than-henry-berry))*

<details>
<summary>Решение</summary>

``` sql
select a.actor_id,  first_name , last_name , count(film_id) as film_count 
from actor a
 join film_actor fa ON a.actor_id = fa.actor_id
group by fa.actor_id
having count(film_id) > (select count(film_id)
from actor a
 join film_actor fa ON a.actor_id = fa.actor_id
where first_name = 'HENRY')
order by 4
```
</details>

*12. Напишите запрос для расчета суммы платежей за каждый месяц и отображения результатов в порядке убывания месяца платежа.  ([ссылка](https://sqltest.online/ru/question/normal/analyze-monthly-payment))*

<details>
<summary>Решение</summary>

``` sql
select  DATE_FORMAT( payment_date, '%Y-%m') AS payment_month ,  sum(amount) as payment_amount
from  payment 
group by 1
order by max(payment_month) desc
```
</details>

*13. Напишите запрос, для нахождения месяца с наибольшей общей суммой платежей из таблицы payment.  ([ссылка](https://sqltest.online/ru/question/normal/find-the-best-month))*

<details>
<summary>Решение</summary>

``` sql
select  DATE_FORMAT( payment_date, '%Y-%m') AS payment_month ,  sum(amount) as payment_amount
from  payment 
group by 1
order by payment_amount desc
limit 1
```
</details>

*14. Напишите запрос, для поиска фильма с наибольшим количеством прокатов в базе данных Sakila, используя таблицы inventory, film и rental  ([ссылка](https://sqltest.online/ru/question/normal/find-the-most-popular-film))*

<details>
<summary>Решение</summary>

``` sql
select title
from film
join inventory using(film_id)
join rental using(inventory_id)
group by film_id
order by count(*) desc 
limit 1
```
</details>

*15. Напишите запрос и получите информацию о количестве прокатов фильма "BUCKET BROTHERHOOD" помесячно.  ([ссылка](https://sqltest.online/ru/question/normal/analyze-rental-data-for-film))*

<details>
<summary>Решение</summary>

``` sql
select f.title as film, DATE_FORMAT(r.rental_date, '%Y-%m') AS rental_month, count(f.film_id) as rental_count
from film f
join inventory i on f.film_id = i.film_id
join rental r on r.inventory_id = i.inventory_id
where title = 'BUCKET BROTHERHOOD'
group by 1, 2
order by 2
```
</details>

*16. Найдите всех сотрудников, занятых на проекте "Video Database".  ([ссылка](https://sqltest.online/ru/question/normal/find-all-employees-works-on-the-project))*

<details>
<summary>Решение</summary>

``` sql
select  e.EMP_NO , e.FIRST_NAME , e.LAST_NAME , e.HIRE_DATE , e.JOB_CODE 
from  EMPLOYEE e 
join    EMPLOYEE_PROJECT ep on e.EMP_NO = ep.EMP_NO
join  PROJECT p on ep.PROJ_ID = p.PROJ_ID and  PROJ_NAME = 'Video Database'
order by 3, 5
```
</details>

*17. Напишите запрос, чтобы найти всех покупателей имеющих оплаченные, но неотправленные заказы.  ([ссылка](https://sqltest.online/ru/question/normal/find-all-customers-with-unshipped-orders))*

<details>
<summary>Решение</summary>

``` sql
select  CUSTOMER , min(ORDER_DATE) as FIRST_ORDER_DATE
from customer c
join sales s on c.cust_no = s.cust_no
where  paid = 'y' and  ORDER_STATUS != 'shipped'
group by 1
order by 2
```
</details>

*18. Найдите самый длинный фильм в таблице film.  ([ссылка](https://sqltest.online/ru/question/normal/get-the-longest-movie))*

<details>
<summary>Решение</summary>

``` sql
select  title , release_year
from film
order by length desc, replacement_cost 
limit 1
```
</details>

*19. выберите название, описание и год выхода фильмов из таблицы film.
Отсортируйте полученный список по названию в алфавитном порядке и выведите десять строк начиная с двадцать первой.   ([ссылка](https://sqltest.online/ru/question/normal/get-films-list-third-page))*

<details>
<summary>Решение</summary>

``` sql
select  title,  description , release_year 
from film
order by 1
limit 10 offset 20
```
</details>

*20. Из фильмов имеющихся в наличии, найдите те которые ни разу не бывшие в прокате.   ([ссылка](https://sqltest.online/ru/question/normal/find-the-films-never-been-rented))*

<details>
<summary>Решение</summary>

``` sql
select f.title
from film f
 join inventory i on f.film_id = i.film_id
 left join rental r on i.inventory_id = r.inventory_id
where rental_date is null 
```
</details>

*21. Найдите клиентов имеющих арендованные и не возвращенные диски.   ([ссылка](https://sqltest.online/ru/question/normal/find-customers-who-did-not-return-rented-discs))*

<details>
<summary>Решение</summary>

``` sql
select distinct first_name, last_name, email
from customer
 join rental using(customer_id)
where   return_date is null 
order by 1, 2
```
</details>

*22. Найдите средний ежедневный прокат фильмов.   ([ссылка](https://sqltest.online/ru/question/normal/find-average-daily-film-rentals))*

<details>
<summary>Решение</summary>

``` sql
SELECT AVG(daily_count) AS daily_average_rents_count
FROM (
    SELECT COUNT(*) AS daily_count
    FROM rental
    GROUP BY DATE(rental_date)
) AS daily_counts;
```
</details>

*23. Рассчитайте ежедневный доход за июль 2005 года.   ([ссылка](https://sqltest.online/ru/question/normal/calculate-daily-income-for-july))*

<details>
<summary>Решение</summary>

``` sql
select date(payment_date) as date, sum(amount) as daily_income
from payment
WHERE payment_date BETWEEN '2005-07-01' AND '2005-08-01'
group by 1
order by 1
```
</details>

*26. Найдите среднюю стоимость проката фильма для каждой категории.   ([ссылка](https://sqltest.online/ru/question/normal/find-the-average-cost-of-renting-a-movie-by-category))*

<details>
<summary>Решение</summary>

``` sql
select name as category, avg(film.rental_rate) as avg_rental_rate
from category
 join  film_category using(category_id)
 join film using(film_id)
group by 1 
order by 2 desc
```
</details>

*28. Найдите все комедии продолжительностью более трёх часов.   ([ссылка](https://sqltest.online/ru/question/normal/find-long-comedies))*

<details>
<summary>Решение</summary>

``` sql
select   f.title ,  f.release_year , f.length 
from film f
 join film_category fc using(film_id)
where f.length > 180 and category_id = (select category_id from category where name = 'Comedy')
group by film_id 
order by f.length
```
</details>
