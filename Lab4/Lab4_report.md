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
![image](https://github.com/user-attachments/assets/f3a58f5b-cb35-49ee-a796-52e70ca59665)    
Вот надо было сразу так


Первой частью лабораторной работы является задание Implementing Basic Forwarding. В нем необходимо выполнить следующие задачи: - В виртуальной машине перейдите в папку проекта и выполните задания описанные в Implementing Basic Forwarding     

Второй частью лабораторной работы является задание Implementing Basic Tunneling В нем необходимо выполнить следующие задачи: - В виртуальной машине перейдите в папку проекта и выполните задания описанные в Implementing Basic Tunneling    

#### Реализация базовой переадресации    
Проверка установленного ПО. Далее нужно проверить, что изначально пинг не поддреживается. Для этого запустим mininet.
```
make run
```
![image](https://github.com/user-attachments/assets/5ef048ab-e917-467a-8973-84fc5342fe2a)    

Пинг не поддерживается:    
![image](https://github.com/user-attachments/assets/af00785a-47fb-409d-bc33-8f511061aa81)    

![image](https://github.com/user-attachments/assets/8419a37f-ca00-44a5-8101-ef9c2b324757)    

![image](https://github.com/user-attachments/assets/94d8c52c-ef91-4efa-a542-d56d27d6ade4)     

![image](https://github.com/user-attachments/assets/deee17eb-604b-4ee0-bd81-ef17aa549ef5)      

![image](https://github.com/user-attachments/assets/1a5d2f7d-a70a-453b-b2c2-66d86a769fa5)     

![image](https://github.com/user-attachments/assets/d6389dad-6489-4bf6-9dc9-ec88d4fc64e5)    

![image](https://github.com/user-attachments/assets/281640f1-f227-4708-a41a-a33ef8c3a34e)    

![image](https://github.com/user-attachments/assets/f60c91fc-f12c-4667-99b3-d94bccbac1be)    

![image](https://github.com/user-attachments/assets/3428ca20-70a9-4f5e-b9ed-68f06c7c99bf)     

![image](https://github.com/user-attachments/assets/4923b097-6554-4f52-95cd-e13e9cc9c7f6)     

![image](https://github.com/user-attachments/assets/e1222968-b866-4a79-b0e8-e71d7af88a07)     

![image](https://github.com/user-attachments/assets/fcfc0200-567f-4bed-b3e8-908d00a44600)     

![image](https://github.com/user-attachments/assets/41b21a5e-7e4f-4e10-87c5-f985a84cba41)     

![image](https://github.com/user-attachments/assets/2f9fa99b-d9e5-47ae-a7e3-c0076448194e)


### Вывод
В ходе данной работы были реализованы базовая переадресация и туннелирование с помощью языка P4


















 
