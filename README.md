# Домашнее задание к занятию "Работа с данными (DDL/DML)" - `Антон Плехов`


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
Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

фамилия и имя сотрудника из этого магазина;
город нахождения магазина;
количество пользователей, закреплённых в этом магазине.
`
```
Решение.

SELECT 
    st.store_id, 
    LOWER(s.last_name) AS employee_last_name, 
    LOWER(s.first_name) AS employee_first_name, 
    LOWER(ci.city) AS store_city, 
    COUNT(c.customer_id) AS customer_count
FROM store st
JOIN staff s ON st.store_id = s.store_id
JOIN address a ON s.address_id = a.address_id
JOIN city ci ON a.city_id = ci.city_id
JOIN customer c ON st.store_id = c.store_id
GROUP BY st.store_id, s.last_name, s.first_name, ci.city
HAVING COUNT(c.customer_id) > 300;

```

`
Скриншоты:
![description](https://github.com/whiskymerchant/sys-pattern-homework/blob/sdb2-3/img/)
`  

---

### Задание 2

`
Задание 2
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.
`

```
SELECT COUNT(*) AS films_above_average
FROM film
WHERE length > (SELECT AVG(length) FROM film);

```

`Скриншоты:

`


---

### Задание 3

`
Задание 3
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.
`


```
SELECT 
    DATE_FORMAT(payment_date, '%Y-%m') AS payment_month, 
    SUM(amount) AS total_payments, 
    COUNT(rental_id) AS rental_count
FROM payment
GROUP BY payment_month
ORDER BY total_payments DESC
LIMIT 1;


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
