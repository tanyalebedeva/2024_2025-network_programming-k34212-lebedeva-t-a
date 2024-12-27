University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Network programming](https://github.com/itmo-ict-faculty/network-programming)  
Year: 2024/2025  
Group: K34212  
Author: Lebedeva Tatyana      
Lab: Lab4  
Date of create: 26.12.2024  
Date of finished: 27.12.2024

## Лабораторная работа №4 "Базовая 'коммутация' и туннелирование используя язык программирования P4"

### Описание
В данной лабораторной работе вы познакомитесь на практике с языком программирования P4, разработанный компанией Barefoot (ныне Intel) для организации процесса обработки сетевого трафика на скорости чипа. Barefoot разработал несколько FPGA чипов для обработки трафика которые были встроенны в некоторые модели коммутаторов Arista и Brocade.

### Цель работы
Изучить синтаксис языка программирования P4 и выполнить 2 задания обучающих задания от Open network foundation для ознакомления на практике с P4.


### Ход работы
Данную лабораторную работу рекомендуется начать с изучения P416 Language Specification, этот документ поможет вам в первоначальном представлении о языке программирования P4.    
#### Поднятие виртуальной машины    
1. Склонировать репозиторий p4lang/tutorials    
   ![image](https://github.com/user-attachments/assets/72fe226d-b322-4c93-bf71-f3da6a96ee04)

3. Установить Vagrant и VirtualBox    
   ![image](https://github.com/user-attachments/assets/61cba581-637b-430f-8877-ca68e1f7e520)

5. Перейти в папку cd vm-ubuntu-20.04    
   ![image](https://github.com/user-attachments/assets/33ac7a4e-785d-4b46-bd06-5262c7e020b7)    

7. Используя Vagrant развернуть тестовую среду vagrant up    
   ![image](https://github.com/user-attachments/assets/42b64e6a-ca0f-4ea8-87bf-a8db1306bc86)
    
В результате установки у вас появится виртуальная машина с аккаунтами login/password vagrant/vagrant и p4/p4    
В итоге ничего не получилось, машина получается сломанная и без пользователя P4, поэтому напрямую скачиваю образ     

Первой частью лабораторной работы является задание Implementing Basic Forwarding. В нем необходимо выполнить следующие задачи: - В виртуальной машине перейдите в папку проекта и выполните задания описанные в Implementing Basic Forwarding     

Второй частью лабораторной работы является задание Implementing Basic Tunneling В нем необходимо выполнить следующие задачи: - В виртуальной машине перейдите в папку проекта и выполните задания описанные в Implementing Basic Tunneling    

#### Реализация базовой переадресации    


 
