# Домашнее задание к занятию "Базы данных" - `Антон Плехов`


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
Опишите не менее семи таблиц, из которых состоит база данных:

какие данные хранятся в этих таблицах;
какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.
Приведите решение к следующему виду:

Сотрудники (

идентификатор, первичный ключ, serial,
фамилия varchar(50),
...
идентификатор структурного подразделения, внешний ключ, integer).
`
```
Решение.

Предлагаю разбить данные на семь таблиц с соответствующими связями:

1. Employees

   employee_id SERIAL PRIMARY KEY
   first_name VARCHAR(50)
   middle_name VARCHAR(50)
   surname VARCHAR(50)
   salary NUMERIC(10, 2)
   position VARCHAR(50)
   hire_date DATE
   branch_id INTEGER REFERENCES Branches(branch_id)
   project_id INTEGER REFERENCES Projects(project_id)

2. Departments

   department_id SERIAL PRIMARY KEY
   department_type VARCHAR(50)
   department_name VARCHAR(100)

3. Branches

   branch_id SERIAL PRIMARY KEY
   region VARCHAR(100)
   city VARCHAR(50)
   street_address VARCHAR(200)
   building VARCHAR(50)

4. Projects

   project_id SERIAL PRIMARY KEY
   project_name VARCHAR(100)

5. Positions

   position_id SERIAL PRIMARY KEY
   position_name VARCHAR(50)

6. Salaries

   salary_id SERIAL PRIMARY KEY
   employee_id INTEGER REFERENCES Employees(employee_id)
   salary_amount NUMERIC(10, 2)
   effective_date DATE

7. Employee_departments (optional - те можно уже в процессе сделать)

   employee_id INTEGER REFERENCES Employees(employee_id),
   department_id INTEGER REFERENCES Departments(department_id),
   PRIMARY KEY (employee_id, department_id)

```

`Скриншоты:
![descrioption](https://github.com/whiskymerchant/sys-pattern-homework/blob/sdb2-1/)
`

---

### Задание 2

`

`

```

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
