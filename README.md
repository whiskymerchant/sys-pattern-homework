# Домашнее задание к занятию "Система мониторинга Zabbix" - `Антон Плехов`


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

`Установите Zabbix Server с веб-интерфейсом.`

1. на одну машину савим полный набор: сервер, агент, веб, на вторую - только агент.

```
Машина 1:
# wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
# dpkg -i zabbix-release_6.0-4+debian11_all.deb
# apt update

# apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-nginx-conf zabbix-sql-scripts zabbix-agent

# sudo -u postgres createuser --pwprompt zabbix
# sudo -u postgres createdb -O zabbix zabbix

# zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

# systemctl restart zabbix-server zabbix-agent nginx php7.4-fpm
# systemctl enable zabbix-server zabbix-agent nginx php7.4-fpm

Машина 2:
# wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
# dpkg -i zabbix-release_6.0-4+debian11_all.deb
# apt update

# apt install zabbix-agent

# systemctl restart zabbix-agent
# systemctl enable zabbix-agent
```

`При необходимости прикрепитe сюда скриншоты
![Авторизация в админке](https://github.com/whiskymerchant/sys-pattern-homework/blob/smon-02/img/Screenshot_2024-06-08_214052.jpg)
`



---

### Задание 2

`Установите Zabbix Agent на два хоста.`

1. Агент установлен на два хоста. Сервер обращается к нему по локалхосту на порте 10050, ко второму агенту - по IP. 

```
Команды для установки агента:

# wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
# dpkg -i zabbix-release_6.0-4+debian11_all.deb
# apt update

# apt install zabbix-agent

# systemctl restart zabbix-agent
# systemctl enable zabbix-agent

Конфиг: sudo nano /etc/zabbix/zabbix_agentd.conf


```

`При необходимости прикрепитe сюда скриншоты
![Configuration -> Hosts](https://github.com/whiskymerchant/sys-pattern-homework/blob/smon-02/img/Screenshot_2024-06-08_214243.jpg)
![Agent's logs](https://github.com/whiskymerchant/sys-pattern-homework/blob/smon-02/img/Screenshot_2024-06-08_214938.jpg)
![Incoming data from both agent and server](https://github.com/whiskymerchant/sys-pattern-homework/blob/smon-02/img/Screenshot_2024-06-08_215132.jpg)

`


---

### Задание 3

`Приведите ответ в свободной форме........`

1. 

```
Поле для вставки кода...
....
....
....
....
```
`При необходимости прикрепитe сюда скриншоты
![]()`

### Задание 4

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`
