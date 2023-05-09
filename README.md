 Домашние задания по модулю «Мониторинг»

 Система мониторинга Zabbix   Ярчак Александр


Задание 1

Установите Zabbix Server с веб-интерфейсом.
Процесс выполнения

    Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
    Установите PostgreSQL. Для установки достаточна та версия что есть в системном репозитороии Debian 11
    Пользуясь конфигуратором комманд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache
    Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server

Требования к результаты

    Прикрепите в файл README.md скриншот авторизации в админке
    Приложите в файл README.md текст использованных команд в GitHub


Решение

Установил zabbix  на вм yandex cloud на debian 11

Настроил zabbix-server конфиг файл (добавил данные по паролю dbpassword)
и в файл конфигурации агента на 2-х машинах добавил ip адрес сервера zabbix


(https://github.com/megawebtech/zabbix/blob/main/zabbix_main_page.png)

![scr]https://github.com/megawebtech/zabbix/blob/main/zabbix_3_hosts.png


Установка на debian 11 полностью из лекции:

1. устанваливаю на сервер postgreql

sudo apt install postgresql

2. скачиваю и добавляю репозиторий. Обнавляю данные по репозиториям.

wget https://repo.zabbix.com/zabbix/6.0/deban/pool/main/z/zabbix-release_6.0-4%2Bdebian11_all.deb

dpkg -i zabbix-release_6.0-4+debian11_all.deb

apt update

3. запускаю zabbix-сервер и агента

sudo apt install zabbix-server-pgsql  zabbix-frontend-php  php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts nano -y  zabbix-agent

4. создаю пользователя базы данных

sudo -u postgres createuser --pwprompt zabbix

5. создаю базу данныx для zabbix

sudo -u postgrez create -O zabbix zabbix

6. импортию схему

zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

7. в файле zabbix_server.conf устанавливаю пароль для zabbix

8. запускаю zabbix-server и агента

sudo systemctl restart zabbix-server apache2 server-agent

  

Задание 2

Установите Zabbix Agent на два хоста.
Процесс выполнения

    Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
    Установите Zabbix Agent на 2 виртмашины, одной из них может быть ваш Zabbix Server
    Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов
    Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera
    Проверьте что в разделе Latest Data начали появляться данные с добавленных агентов

Требования к результаты

    Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
    Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
    Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
    Приложите в файл README.md текст использованных команд в GitHub



Агент zabbix установил на другую виртуальную машину (по аналогии с установкой сервера).
Т.е. установил на машину агента без установки postgres.



Скриншот что агенты подключены к серверу:

https://github.com/megawebtech/zabbix/blob/main/zabbix%20agents%202.png


 Агент zabbix работает:


https://github.com/megawebtech/zabbix/blob/main/agent%20is%20working.png


Данные по последним данным (видно сколько секунд назад данные были обновлены:

https://github.com/megawebtech/zabbix/blob/main/latest%20data%20monitor.png


