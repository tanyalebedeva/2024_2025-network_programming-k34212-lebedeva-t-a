Faculty: [FICT](https://fict.itmo.ru)

Course: [Network programming](https://github.com/itmo-ict-faculty/network-programming)

Year: 2024/2025

Group: K34212

Author: Lebedeva Tatiana Alexandrovna

Lab: Lab3

Date of create: 01.12.2024

Date of finished: 07.12.2024

# Лабораторная работа №3 "Развертывание Netbox, сеть связи как источник правды в системе технического учета Netbox"

## Описание
В данной лабораторной работе вы ознакомитесь с интеграцией Ansible и Netbox и изучите методы сбора информации с помощью данной интеграции.

## Цель работы
С помощью Ansible и Netbox собрать всю возможную информацию об устройствах и сохранить их в отдельном файле.

## Ход работы
Инструкция по установке NetBox IRM на Ubuntu 24.04.1 LTS: https://dzen.ru/a/ZxpR4ABlFzJRNJyn    

1. Поднять Netbox на дополнительной VM.
   Шаг 1 – Установить PostgreSQL Server
   NetBox использует PostgreSQL в качестве ядра базы данных, поэтому нужно установить его на свой сервер. Можно установить его с помощью следующей команды.
   ```
   apt update -y
   apt install postgresql postgresql-contrib -y
   ```
   
   Далее проверить работу сервиса PostgreSQL.
   ```
   systemctl status postgresql
   ```
   Далее авторизоваться в PostgreSQL.
   ```
   sudo -i -u postgres psql
   ```
   Создание базы данных и пользователя для Netbox.
   ![image](https://github.com/user-attachments/assets/e580fb46-7460-4b68-bb64-7765c965d285)

   Шаг 2 – Установить Redis
   NetBox использует Redis для кэширования, поэтому вам нужно будет установить его на свой сервер. Вы можете установить его с помощью следующей команды.
   ```
   apt install redis -y
   ```
   Можно проверить установку Redis с помощью следующей команды.
   ```
   redis-server -v
   ```
   ![image](https://github.com/user-attachments/assets/b82d77d3-9149-412f-9333-af38350dc93c)

   Шаг 3 – Установка Netbox
   Необходимо установить все необходимые зависимости.
   ```
   apt install -y python3 python3-pip python3-venv python3-dev build-essential libxml2-dev libxslt1-dev libffi-dev libpq-dev libssl-dev zlib1g-dev
   ```
   Далее необходимо создать директорию для NetBox.
   ```
   mkdir -p /opt/netbox/
   ```
   Затем изменить каталог на NetBox и загрузите последнюю версию NetBox из репозитория Git.
   ```
   cd /opt/netbox
   git clone -b master —depth 1 https://github.com/netbox-community/netbox.git .
   git config —global —add safe.directory /opt/netbox
   ```
   ![image](https://github.com/user-attachments/assets/f0406f0c-fd23-49f2-a8ed-707c12872ff8)
   
   Далее создать пользователя и группу для NetBox.
   ```
   adduser —system —group netbox
   ```    
   Изменить владельца каталога NetBox.
   ```
   chown —recursive netbox /opt/netbox
   chown —recursive netbox /opt/netbox/netbox/media/
   ```
   
   Затем переименовть пример файла конфигурации NetBox.
   ```
   cd /opt/netbox/netbox/netbox/    
   cp configuration_example.py configuration.py
   ```
   Затем сгенерировать секретный ключ.
   ```
   python3 ../generate_secret_key.py   
   ```    
   Далее отредактировать файл конфигурации NetBox.nano configuration.py    
   ![image](https://github.com/user-attachments/assets/f752a06b-4c16-4019-88b6-31fc944e64cf)    
   ![image](https://github.com/user-attachments/assets/55c0ffb1-83b7-4316-8a99-c059bcafe67d)
   Сохранить и закрыть файл, затем установить NetBox с помощью следующей команды.
   ```
   /opt/netbox/upgrade.sh
   ```
   Шаг 4 – Создать пользователя Netbox Admin
   ```
   source /opt/netbox/venv/bin/activate
   ```
   Далее необходимо создать суперпользователя для NetBox.
   ```
   cd /opt/netbox/netbox
   python3 manage.py createsuperuser
   ```
   Далее необохдимо создать символическую ссылку на служебный файл NetBox.
   ```
   ln -s /opt/netbox/contrib/netbox-housekeeping.sh /etc/cron.daily/netbox-housekeeping
   ```
   
   ![image](https://github.com/user-attachments/assets/e236cb10-310c-49ee-b266-76eecffa49bb)    

   Шаг 5 – Запустить сервер Netbox
   Запустить сервер NetBox с помощью следующей команды.
   ```
   python3 manage.py runserver 0.0.0.0:8000 —insecure
   ```
   ![image](https://github.com/user-attachments/assets/3738afd4-27c7-452a-892f-3ed19a24d73d)

   Пробрасываем нужные порты в VirtualBox, открываем браузер и переходим по ссылке https://0.0.0.0:8000
   ![image](https://github.com/user-attachments/assets/a10796c5-8e36-43e2-ba87-b1d2efd7431f)
   ![image](https://github.com/user-attachments/assets/e8a1941f-7021-4ce6-bbcf-bfb385ecb292)

3. Заполнить всю возможную информацию о ваших CHR в Netbox.
   
5. Используя Ansible и роли для Netbox в тестовом режиме сохранить все данные из Netbox в отдельный файл, результат приложить в отчёт.
   
7. Написать сценарий, при котором на основе данных из Netbox можно настроить 2 CHR, изменить имя устройства, добавить IP адрес на устройство.
   
9. Написать сценарий, позволяющий собрать серийный номер устройства и вносящий серийный номер в Netbox.
