# Домашнее задание к занятию "Индексы" - `Антон Плехов`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

`
Напишите запрос к учебной базе данных, который вернёт процентное отношение общего размера всех индексов к общему размеру всех таблиц.
`
```
Решение.

SELECT 
    ROUND(SUM(INDEX_LENGTH) / SUM(DATA_LENGTH + INDEX_LENGTH) * 100, 2) AS "Процент индекса"
FROM 
    information_schema.TABLES
WHERE 
    TABLE_NAME IN ('actor', 'address', 'category', 'city', 'country', 'customer', 
                   'film', 'film_actor', 'film_category', 'film_text', 
                   'inventory', 'language', 'payment', 'rental', 'staff', 'store')
    AND TABLE_SCHEMA = 'sakila';

```

`
Скриншоты:
![description](https://github.com/whiskymerchant/sys-pattern-homework/blob/sdb2-3/img/)
`  

---

### Задание 2

`
Выполните explain analyze следующего запроса:

select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount) over (partition by c.customer_id, f.title)
from payment p, rental r, customer c, inventory i, film f
where date(p.payment_date) = '2005-07-30' and p.payment_date = r.rental_date and r.customer_id = c.customer_id and i.inventory_id = r.inventory_id

перечислите узкие места;
оптимизируйте запрос: внесите корректировки по использованию операторов, при необходимости добавьте индексы.
`

```
Решение

1. Запрос выполняется долго:
-> Table scan on <temporary>  (cost=2.5..2.5 rows=0) (actual time=2186..2186 rows=391 loops=1)
    -> Temporary table with deduplication  (cost=0..0 rows=0) (actual time=2186..2186 rows=391 loops=1)
        -> Window aggregate with buffering: sum(payment.amount) OVER (PARTITION BY c.customer_id,f.title )   (actual time=970..2103 rows=642000 loops=1)
            -> Sort: c.customer_id, f.title  (actual time=970..997 rows=642000 loops=1)
                -> Stream results  (cost=21.7e+6 rows=16e+6) (actual time=0.77..756 rows=642000 loops=1)
                    -> Nested loop inner join  (cost=21.7e+6 rows=16e+6) (actual time=0.762..662 rows=642000 loops=1)
                        -> Nested loop inner join  (cost=20.1e+6 rows=16e+6) (actual time=0.753..558 rows=642000 loops=1)
                            -> Nested loop inner join  (cost=18.5e+6 rows=16e+6) (actual time=0.743..454 rows=642000 loops=1)
                                -> Inner hash join (no condition)  (cost=1.58e+6 rows=15.8e+6) (actual time=0.706..21.8 rows=634000 loops=1)
                                    -> Filter: (cast(p.payment_date as date) = '2005-07-30')  (cost=1.65 rows=15813) (actual time=0.0533..2.51 rows=634 loops=1)
                                        -> Table scan on p  (cost=1.65 rows=15813) (actual time=0.0374..1.85 rows=16044 loops=1)
                                    -> Hash
                                        -> Covering index scan on f using idx_title  (cost=103 rows=1000) (actual time=0.126..0.452 rows=1000 loops=1)
                                -> Covering index lookup on r using rental_date (rental_date=p.payment_date)  (cost=0.969 rows=1.01) (actual time=460e-6..597e-6 rows=1.01 loops=634000)
                            -> Single-row index lookup on c using PRIMARY (customer_id=r.customer_id)  (cost=250e-6 rows=1) (actual time=63.6e-6..79.5e-6 rows=1 loops=642000)
                        -> Single-row covering index lookup on i using PRIMARY (inventory_id=r.inventory_id)  (cost=250e-6 rows=1) (actual time=63.2e-6..79e-6 rows=1 loops=642000)
2. Узкие места:
(а) Джойны по таблицам
(б) Использование функции DATE
(в) PARTITION BY c.customer_id, f.title
3. Такой запрос выполняется за 10 мс:
EXPLAIN ANALYZE
SELECT DISTINCT CONCAT(c.last_name, ' ', c.first_name), 
                SUM(p.amount) OVER (PARTITION BY c.customer_id) AS total_amount
FROM payment p
INNER JOIN rental r ON p.payment_date = r.rental_date
INNER JOIN customer c ON r.customer_id = c.customer_id
INNER JOIN inventory i ON r.inventory_id = i.inventory_id
INNER JOIN film f ON i.film_id = f.film_id
WHERE p.payment_date >= '2005-07-30 00:00:00' 
  AND p.payment_date < '2005-07-31 00:00:00';EXPLAIN ANALYZE
SELECT DISTINCT CONCAT(c.last_name, ' ', c.first_name), 
                SUM(p.amount) OVER (PARTITION BY c.customer_id) AS total_amount
FROM payment p
INNER JOIN rental r ON p.payment_date = r.rental_date
INNER JOIN customer c ON r.customer_id = c.customer_id
INNER JOIN inventory i ON r.inventory_id = i.inventory_id
INNER JOIN film f ON i.film_id = f.film_id
WHERE p.payment_date >= '2005-07-30 00:00:00' 
  AND p.payment_date < '2005-07-31 00:00:00';
```

`Скриншоты:

`


---

### Задание 3

`

`


```
```
`Скриншоты:

`

### Задание 4

`

`


```
```

`Скриншоты:

`
