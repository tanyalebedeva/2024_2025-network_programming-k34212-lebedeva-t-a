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
   ![image](https://github.com/user-attachments/assets/1b024b8f-f46c-4ca3-9607-350f0cb23fa4)    

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
   ![image](https://github.com/user-attachments/assets/6da1728b-8ff5-42aa-a2b8-858c9555c2ee)    

   Шаг 3 – Установка Netbox
   Необходимо установить все необходимые зависимости.
   ```
   apt install -y python3 python3-pip python3-venv python3-dev build-essential libxml2-dev libxslt1-dev libffi-dev libpq-dev libssl-dev zlib1g-dev
   ```
   ![image](https://github.com/user-attachments/assets/646d7fe8-097d-4fa0-8472-35e15708f26a)    

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
   ![image](https://github.com/user-attachments/assets/7928fac3-564f-45d4-9a50-500fc551fb42)
   ![image](https://github.com/user-attachments/assets/f93a94d1-9954-4f5a-a178-17cd32bdf3fd)
   ![image](https://github.com/user-attachments/assets/8f7bced8-5091-4eb5-937f-9f5f2d491a48)
   ![image](https://github.com/user-attachments/assets/1001dd57-1374-4af9-a60e-8854e4eea2c5)
   ![image](https://github.com/user-attachments/assets/11e47a0d-e090-463a-9927-9848547fd676)    
   ![image](https://github.com/user-attachments/assets/084a802b-fe2e-43c9-bf60-b7a3df4b01af)
   ![image](https://github.com/user-attachments/assets/1957e55d-0d26-47fd-bb36-cdcc7adb0beb)
   ![image](https://github.com/user-attachments/assets/90a71663-9a8c-488e-a527-14e5f7e0b687)

4.  Используя Ansible и роли для Netbox в тестовом режиме сохранить все данные из Netbox в отдельный файл, результат приложить в отчёт.
   Роль fetch_info для сбора данных и сохранения их в файл:
   ![image](https://github.com/user-attachments/assets/1589700c-16e8-4ce7-b45d-69dcf2211806)
   Плейбук playbook.yaml:
   ![image](https://github.com/user-attachments/assets/aa085758-5150-4642-8b41-4b87a6c7fe99)
   Выполнение плейбука:
   ![image](https://github.com/user-attachments/assets/af666eb8-2154-49f6-88a1-71e0892b8d88)
   Произведена запись данных из NetBox в netbox_devices.json:
   ![image](https://github.com/user-attachments/assets/f7d4bd81-1ac1-4d3d-94f2-aca0ce6ca54c)
   Итоговый файл представлен в репозитории.

5. Написать сценарий, при котором на основе данных из Netbox можно настроить 2 CHR, изменить имя устройства, добавить IP адрес на устройство.
   Файл inventory.yaml:
   ![image](https://github.com/user-attachments/assets/698c1784-81a0-417e-a384-5004f6882f39)
   Плейбук для изменения настроек роутера в соответствии с данными из NetBox:
   ![image](https://github.com/user-attachments/assets/8f186448-fc89-4fbe-b4f4-ecc9190a2f54)
   ![image](https://github.com/user-attachments/assets/b319640c-de3e-4e4b-9e9a-fd5ba405db1f)
   Выполнение плейбука:
   ![image](https://github.com/user-attachments/assets/30d4d032-f140-45b4-a944-3d387ee2625a)
   В результате выполнения плейбука были произведены изменения ip-адреса интерфеса ether3, а так же изменено название устройства    
   Добавление IP-адреса 192.168.0.90/24:
   ![image](https://github.com/user-attachments/assets/95bc8f3c-a764-4e6a-b036-7f5204bb1a09)
   Изменение имени устройства с MikroTik на CHR2:
   ![image](https://github.com/user-attachments/assets/b26d027b-63f4-4b78-83d7-899f319a0826)
   Полученный IP-адрес совпадает с адресом на NetBox:
   ![image](https://github.com/user-attachments/assets/aa6cb802-94bc-435d-894f-137b92611720)
   
6. Написать сценарий, позволяющий собрать серийный номер устройства и вносящий серийный номер в Netbox.
   Получен серийный номер устройства:
   ![image](https://github.com/user-attachments/assets/fe3d9158-ed9c-4d1b-b98f-fcb1de8dd09a)    
   Плейбук для добавления серийного номера в NetBox:
   ![image](https://github.com/user-attachments/assets/b879ff0e-4ee7-4b55-ab32-b16da66a99c9)
   ![image](https://github.com/user-attachments/assets/829664cd-c5f6-4615-9aec-7bf6ed61e7b4)
   Выполнение плейбука:
   ![image](https://github.com/user-attachments/assets/5fc7b00e-8e46-4f44-acec-624ad9dcbedd)
   ![image](https://github.com/user-attachments/assets/2e8f3e9a-6e94-41f0-b1fb-3d5319345d2a)
   Результат добавления серийного номера в NetBox:
   ![image](https://github.com/user-attachments/assets/8d7285b2-4284-4ef9-8c30-5cdd37055a48)

## Выводы
В ходе работы был настроен Ansible с NetBox





