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
В связи с проблемами с доступом к Microsoft Azure, а также с отсуствием бесплатных аналогов, в качесвте сервера была использована виртуальная машина Ubuntu 24.04 на Oracle Virtual box.    
![image](https://github.com/user-attachments/assets/83f8f3bd-d4f7-437b-8d32-072c74e3a326)
Обновлена операционнная система с помощью следующих команд:    
```
sudo apt update & sudo apt upgrade
sudo do-release-upgrade
```
Далеее установлены python3 и Ansible:    
```
sudo apt install python3-pip
ls -la /usr/bin/python3.6
sudo pip3 install ansibl
```
![image](https://github.com/user-attachments/assets/5979cb2d-64ff-4a03-b07c-d3f5a88babeb)    

Установлен Wireguard c помощью команды:    
```
sudo apt install wireguard
```
![image](https://github.com/user-attachments/assets/5347abb2-3b64-46b3-8e39-5ba7d5dbd295)    

Сгенерирован приватный ключ на сервере с помошью команды:    
```
wg genkey | tee privatekey
```

Далее сгенерирован публичный ключ с помощью команды:    
```
cat privatekey | wg pubkey | tee publickey
```
![image](https://github.com/user-attachments/assets/936f01e3-ddfa-4da2-8f81-f5fd9f5119f0)    







