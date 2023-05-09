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

  
