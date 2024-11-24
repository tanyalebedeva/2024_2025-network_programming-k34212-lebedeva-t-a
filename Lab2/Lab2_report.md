University: [ITMO University](https://itmo.ru/ru/)

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
1. Установить второй CHR на своем ПК.
2. Организовать второй WireGuard Client на втором CHR.
3. Используя Ansible, настроить сразу на 2-х CHR:

логин/пароль;

NTP Client;

OSPF с указанием Router ID; 4. Собрать данные по OSPF топологии и полный конфиг устройства.

Что использовать: routeros_facts, routeros_commands.

Результаты лабораторной работы
В результате данной работы у вас должно быть:

2 файла с конфигурациями устройств
Схема связи нарисованная вами в draw.io или Visio.
Результаты пингов, проверки локальной связности.
