University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Network programming](https://github.com/itmo-ict-faculty/network-programming)

Year: 2024/2025

Group: K34212

Author: Lebedeva Tatiana Alexandrovna

Lab: Lab1

Date of create: 30.09.2024

Date of finished: 14.10.2024

# Лабораторная работа №1 "Установка CHR и Ansible, настройка VPN"

## Описание
Данная работа предусматривает обучение развертыванию виртуальных машин (VM) и системы контроля конфигураций Ansible а также организации собственных VPN серверов.

## Цель работы
Целью данной работы является развертывание виртуальной машины на базе платформы Microsoft Azure с установленной системой контроля конфигураций Ansible и установка CHR в VirtualBox.

## Ход работы
1. В связи с проблемами с доступом к Microsoft Azure, а также с отсуствием бесплатных аналогов, в качесвте сервера была использована виртуальная машина Ubuntu 24.04 на Oracle Virtual box.

![image](https://github.com/user-attachments/assets/83f8f3bd-d4f7-437b-8d32-072c74e3a326)
3. Обновлена операционнная система с помощью следующих команд:    
```
sudo apt update & sudo apt upgrade
sudo do-release-upgrade
```
3. Далеее установлены python3 и Ansible:    
```
sudo apt install python3-pip
ls -la /usr/bin/python3.6
sudo pip3 install ansibl
```
![image](https://github.com/user-attachments/assets/5979cb2d-64ff-4a03-b07c-d3f5a88babeb)    

4. Установлен Wireguard c помощью команды:    
```
sudo apt install wireguard
```

![image](https://github.com/user-attachments/assets/5347abb2-3b64-46b3-8e39-5ba7d5dbd295)    

5. Сгенерирован приватный ключ на сервере с помошью команды:    
```
wg genkey | tee privatekey
```

Далее сгенерирован публичный ключ с помощью команды:    
```
cat privatekey | wg pubkey | tee publickey
```
![image](https://github.com/user-attachments/assets/936f01e3-ddfa-4da2-8f81-f5fd9f5119f0)    

7. В качестве VPN клиента использован CHR (RouterOS).    
   
![image](https://github.com/user-attachments/assets/3321e003-9d66-4ff9-b79b-8f2fca662b36)    

![image](https://github.com/user-attachments/assets/a82fbf21-73fb-4168-92ef-d18dda0a24b9)    

8. Для настройки клиента необходимо было подключиться к роутеру через WinBox.

![image](https://github.com/user-attachments/assets/226c3fca-065b-4dca-82df-e4286fa9180d)

На WinBox был создан интерфейс Wireguard wg0, на котором были сформированы приватный и публичный ключи клиента.    

![image](https://github.com/user-attachments/assets/75c55ece-ee53-4e4a-9b46-4c806551f272)   

Созданному интерфейсу был присвоен IP-адрес.    

![image](https://github.com/user-attachments/assets/4ac57128-7901-4342-ab17-523d30c5d8b2)


9. На сервере был создан конфигурационный файл для настройки VPN-туннеля, куда в Peer необходимо ввести публичный ключ клиента.
```
GNU nano 7.2 /etc/wireguard/wg0.conf
[Interface]
PrivateKey = aBsClDOOaWYdCFZHXfgOc4BgsA+s/cnx8k8MF6GzT2Y=Address = 10.14.14.1/24
ListenPort = 13231
[Peer]PublicKey = sQ1artOIv6FbZ93MMQ2hZKqPbwdiwLK3Kjm4yfF43g8=
AllowedIPs = 10.14.14.2/24
```    
![image](https://github.com/user-attachments/assets/363505e1-6bd3-4170-9a28-f8180c8b5d4f)

10. На клиенте в разделе Wireguard был создан peer, в котором необходимо было ввести публичный ключ сфрмированный на сервере, настройки VPN.

![image](https://github.com/user-attachments/assets/a70a6584-ed0a-4d44-b0cf-f1e9ed702c83)
В Endpoint нужно ввести внешний адрес сервера, котоорый можно узнать с помощью команды:
```
ip a
```    

![image](https://github.com/user-attachments/assets/f5c09091-14a3-497e-8634-9270313ab29a)
    
11. Также на сервере необходимо запустить службу с помощью команды:
```
sudo systemctl start wg-quick@wg0
sudo systemctl status wg-quick@wg0
```
        
![image](https://github.com/user-attachments/assets/5379f7e5-f006-4510-8b56-5fafdd249fe2)
     
### Тестирование результатов
Проверка доступонсти клиента с сервера    
![image](https://github.com/user-attachments/assets/73f1394d-facd-4fcd-889e-4040fbe074a5)    

Проверка доступности сервера    

![image](https://github.com/user-attachments/assets/13e68f5e-e174-4ff5-a631-8ea62318d90f)

## Выводы
### В ходе выполнения лабораторной работы были выполнены следующие шаги:
#### Развертывание виртуальных машин:
Виртуальная машина с Ubuntu 24.04 была успешно развернута в VirtualBox вместо Microsoft Azure из-за ограничений в доступе к облачным сервисам. На сервере был установлен Ansible для автоматизации задач управления конфигурациями.
Установка и настройка WireGuard:
На сервере был установлен и настроен WireGuard для создания VPN-сервера. Были сгенерированы ключи, создан конфигурационный файл и настроен интерфейс для связи по VPN.
На клиенте CHR 7.16 (RouterOS) также был настроен WireGuard для работы в качестве VPN-клиента. Указаны необходимые параметры, включая публичный ключ, IP-адрес и порт сервера.
##### Сетевая настройка:
Сервер использовал сетевую конфигурацию NAT, а клиент был подключен через сетевой мост. Это привело к необходимости настройки маршрутов и проверки сетевой доступности между клиентом и сервером.
Были проведены проверки сетевой связности и корректности маршрутизации, включая команды ping и wg show. Столкнулись с проблемой "key not available," что было связано с отсутствием корректной настройки пиров.
##### Исправление ошибок:
На сервере и клиенте были проверены сетевые интерфейсы и маршруты. Проблема с недоступностью пиров была решена путём корректной настройки IP-адресов и привязки к интерфейсам, а также использованием корректных портов на обоих устройствах.
##### Тестирование VPN-туннеля:
После успешной настройки VPN сервер и клиент были соединены по туннелю WireGuard. Проверка пиров через команду wg show подтвердила наличие установленного соединения.
Тестирование пингом между клиентом и сервером прошло успешно, подтвердив работу туннеля и IP-связности.
##### Заключение:
Лабораторная работа позволила освоить процесс настройки VPN на базе WireGuard между сервером и клиентом CHR в виртуальной среде. Были решены проблемы с сетью, маршрутами и пирами.










