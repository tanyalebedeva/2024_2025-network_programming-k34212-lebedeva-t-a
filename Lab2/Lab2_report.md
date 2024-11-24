Faculty: [FICT](https://fict.itmo.ru)

Course: [Network programming](https://github.com/itmo-ict-faculty/network-programming)

Year: 2024/2025

Group: K34212

Author: Lebedeva Tatiana Alexandrovna

Lab: Lab1

Date of create: 24.10.2024

Date of finished: 24.11.2024

# Лабораторная работа №2 "Развертывание дополнительного CHR, первый сценарий Ansible"

## Описание
В данной лабораторной работе вы на практике ознакомитесь с системой управления конфигурацией Ansible, использующаяся для автоматизации настройки и развертывания программного обеспечения.

## Цель работы
С помощью Ansible настроить несколько сетевых устройств и собрать информацию о них. Правильно собрать файл Inventory.

## Ход работы
1. Установлен второй CHR на Oracle VM VirtualBox:
   ![image](https://github.com/user-attachments/assets/d0c94236-0475-463a-a957-b76d0632dadc)    
2. Организован второй WireGuard Client на втором CHR.
   
   На созданном роутере CHR2 был настроен Wireguard интерфейс:    
   ![image](https://github.com/user-attachments/assets/f5627c2f-0e37-4de0-a709-b6468c4eb785)
    
   Обновлен файл конфигурации на самом сервере, была добавлена информация о новом клиенте с адресом 10.14.14.3:
   
   ![image](https://github.com/user-attachments/assets/21bd3c1f-a41f-480b-8ea5-22d477d512c1)
   
   Проверка доступности сервера с первого и второго CHR:
   ![image](https://github.com/user-attachments/assets/f03002d6-6c34-43b8-9d93-d8ebede1f4a0)

3. Был создан файл inventory.yaml, содержащий информацию об узлах, на которых следует производить настройку:
   ![image](https://github.com/user-attachments/assets/99119bec-c107-4ddb-b681-d339df9e9f98)

   Он же измененный, после удаления пользователя admin:    
   ![image](https://github.com/user-attachments/assets/2dfd76bb-5eeb-4739-8e02-17996f5406b0)


5. Используя Ansible, настроить сразу на 2-х CHR:

логин/пароль;

NTP Client;

OSPF с указанием Router ID; 4. Собрать данные по OSPF топологии и полный конфиг устройства.

Что использовать: routeros_facts, routeros_commands.

Результаты лабораторной работы
В результате данной работы у вас должно быть:

2 файла с конфигурациями устройств
Схема связи нарисованная вами в draw.io или Visio.
Результаты пингов, проверки локальной связности.
