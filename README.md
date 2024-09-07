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
Задание можно выполнить как в любом IDE, так и в командной строке.

Задание 1
Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

Задание 2
Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.

Задание 3
Получите последние пять аренд фильмов.

Задание 4
Одним запросом получите активных покупателей, имена которых Kelly или Willie.

Сформируйте вывод в результат таким образом:

все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
замените буквы 'll' в именах на 'pp'.
`
```
Решение.

SELECT DISTINCT district 
FROM address
WHERE district LIKE 'K%a' 
AND district NOT LIKE '% %';

SELECT payment_id , amount, payment_date, last_update 
FROM payment
WHERE payment_date BETWEEN '2005-06-15' AND '2005-06-18'
AND amount > 10.00;

SELECT * 
FROM rental
ORDER BY rental_date DESC
LIMIT 5;

SELECT LOWER(REPLACE(REPLACE(first_name, 'll', 'pp'), 'LL', 'PP')) AS Имя,
       LOWER(last_name) AS Фамилия
FROM customer
WHERE first_name IN ('Kelly', 'Willie')
AND active = 1;
```

`
Скриншоты:
![description](https://github.com/whiskymerchant/sys-pattern-homework/blob/sdb2-3/img/)
`  

---

### Задание 2

`

`

```
Решение

Название таблицы|Название первичного ключа|
----------------+-------------------------+
actor           |actor_id                 |
address         |address_id               |
category        |category_id              |
city            |city_id                  |
country         |country_id               |
customer        |customer_id              |
film            |film_id                  |
film_actor      |actor_id                 |
film_actor      |film_id                  |
film_category   |film_id                  |
film_category   |category_id              |
film_text       |film_id                  |
inventory       |inventory_id             |
language        |language_id              |
payment         |payment_id               |
rental          |rental_id                |
staff           |staff_id                 |
store           |store_id                 |

В БД есть таблицы с ключом, по которому нет связи. Видимо его нельзя назвать ПРАЙМЕРИ?

SHOW TABLES

SELECT 
    TABLE_NAME AS 'Название таблицы',
    COLUMN_NAME AS 'Название первичного ключа'
FROM 
    information_schema.KEY_COLUMN_USAGE
WHERE 
    CONSTRAINT_NAME = 'PRIMARY' 
    AND TABLE_SCHEMA = 'sakila';

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
