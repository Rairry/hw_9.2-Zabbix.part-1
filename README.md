# Домашнее задание к занятию 9.2 «Zabbix. Часть 1»


### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

 ---

### Задание 1 

Установите Zabbix Server с веб-интерфейсом.

*Приложите скриншот авторизации в админке.*
<br>

![image](https://user-images.githubusercontent.com/124167007/220482791-e60c1542-7fe6-4b20-8b42-3a7c8b52dfa2.png)

<br> *Приложите текст использованных команд в GitHub.*

apt install postgresql
<br> wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
<br> dpkg -i zabbix-release_6.0-4+debian11_all.deb
<br> apt update
<br> apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
<br> su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'123456789\'';"'
<br> su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'
<br> zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
<br> sudo nano /etc/zabbix/zabbix_server.conf
<br> systemctl restart zabbix-server apache2 # zabbix-agentsudo
<br> systemctl enable zabbix-server apache2 # zabbix-agent

---

### Задание 2 

Установите Zabbix Agent на два хоста.

*Приложите скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу.*

![image](https://user-images.githubusercontent.com/124167007/220699859-d2e85dad-6c04-43cf-b733-8d850825169e.png)

<br> *Приложите скриншот лога zabbix agent, где видно, что он работает с сервером.*

![image](https://user-images.githubusercontent.com/124167007/220699123-4c943bd9-c9fa-4fd9-99ba-f8b278e092ec.png)

<br> *Приложите скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.*

![image](https://user-images.githubusercontent.com/124167007/220699521-80d9798d-29a5-4f13-be59-85833680af7d.png)

<br> *Приложите текст использованных команд в GitHub.*

<br> wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
<br> dpkg -i zabbix-release_6.0-4+debian11_all.deb
<br> apt update
<br> apt install zabbix-agent
<br> systemctl restart zabbix-agent
<br> nano /etc/zabbix/zabbix_agentd.conf
<br> systemctl restart zabbix-agent.service
<br> tail -f /var/log/zabbix/zabbix_agentd.log

---
## Задание со звёздочкой*

Это дополнительное задание. Его выполнять не обязательно. На зачёт это не повлияет. Вы можете его выполнить, если хотите глубже разобраться в материале.

### Задание 3* 

Установите Zabbix Agent на Windows (компьютер) и подключите его к серверу Zabbix.

*Приложите скриншот раздела Latest Data, где видно свободное место на диске C:*
