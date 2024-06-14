# Домашнее задание к занятию "Система мониторинга Zabbix часть 2" - `Антон Плехов`


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

`Создайте свой шаблон, в котором будут элементы данных, мониторящие загрузку CPU и RAM хоста.`

1. Делаем шаблон с двумя items внутри (третий item остался от теста, показанного в лекции).

```

```

`Скриншоты:
![Шаблон с кастомными items](https://github.com/whiskymerchant/sys-pattern-homework/blob/smon-03/img/Screenshot 2024-06-14 134216.jpg)
`



---

### Задание 2

`Добавьте в Zabbix два хоста и задайте им имена <фамилия и инициалы-1> и <фамилия и инициалы-2>. Например: ivanovii-1 и ivanovii-2.`

1. Latest data начала появляться 

```
```

`Скриншоты:
![2 hosts added](https://github.com/whiskymerchant/sys-pattern-homework/blob/smon-03/img/Screenshot 2024-06-14 143003.jpg)
`


---

### Задание 3

`Привяжите созданный шаблон к двум хостам. Также привяжите к обоим хостам шаблон Linux by Zabbix Agent.`

1. Две группы гостов добавлены и собирают информацию

```
```
`Скриншоты:
![1 groups added](https://github.com/whiskymerchant/sys-pattern-homework/blob/smon-03/img/Screenshot 2024-06-14 143003.jpg)`

### Задание 4

`Создайте свой кастомный дашборд.`
1. Будем измерять два важных параментра - загрузка CPU и RAM


```
```

`Скриншоты:
![Custom dashboard](https://github.com/whiskymerchant/sys-pattern-homework/blob/smon-03/img/Screenshot 2024-06-14 150854.jpg)`
