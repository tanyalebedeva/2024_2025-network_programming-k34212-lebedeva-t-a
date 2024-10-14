University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Network programming](https://github.com/itmo-ict-faculty/network-programming)

Year: 2024/2025

Group: K34212

Author: Lebedeva Tatiana Alexandrovna

Lab: Lab1

Date of create: 

Date of finished: 14.10.2024

# Лабораторная работа №1 "Установка CHR и Ansible, настройка VPN"

## Описание
Данная работа предусматривает обучение развертыванию виртуальных машин (VM) и системы контроля конфигураций Ansible а также организации собственных VPN серверов.

## Цель работы
Целью данной работы является развертывание виртуальной машины на базе платформы Microsoft Azure с установленной системой контроля конфигураций Ansible и установка CHR в VirtualBox.

## Ход работы
### Настройка сервера
В связи с проблемами с доступом к Microsoft Azure, а также с отсуствием бесплатных аналогов, в качесвте сервера была использована виртуальная машина Ubuntu 24.04 на Oracle Virtual box.    
![image](https://github.com/user-attachments/assets/83f8f3bd-d4f7-437b-8d32-072c74e3a326)
Обновить операционнцю систему можно с помощью следующих команд:    
```
sudo apt update & sudo apt upgrade
sudo do-release-upgrade
```
Далеее необходимо установить python3 и Ansible:    
```
sudo apt install python3-pip
ls -la /usr/bin/python3.6
sudo pip3 install ansibl
```
![image](https://github.com/user-attachments/assets/5979cb2d-64ff-4a03-b07c-d3f5a88babeb)





