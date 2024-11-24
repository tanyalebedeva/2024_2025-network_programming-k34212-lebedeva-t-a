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
    
3. Обновлен файл конфигурации на самом сервере, была добавлена информация о новом клиенте с адресом 10.14.14.3:
   
   ![image](https://github.com/user-attachments/assets/21bd3c1f-a41f-480b-8ea5-22d477d512c1)
   
   Проверка доступности с сервера первого и второго CHR:
   ![image](https://github.com/user-attachments/assets/f03002d6-6c34-43b8-9d93-d8ebede1f4a0)

   Проверка доступности сервера с первого и второго CHR:

   ![image](https://github.com/user-attachments/assets/001b729f-e6fa-49bc-9172-bf4cbf4f9ab3)
   ![image](https://github.com/user-attachments/assets/7bef51d1-6a71-4fce-a10d-d90301b199fb)    

   Проверка доступности CHR-1 -> CHR-2:
   ![image](https://github.com/user-attachments/assets/13119f8b-2f38-4c7c-9662-296aed55f7d1)    

   Проверка доступности CHR-2 -> CHR-1:
   ![image](https://github.com/user-attachments/assets/f0146775-8ff1-4c86-973c-69cfb3a340aa)


4. Был создан файл inventory.yaml, содержащий информацию об узлах, на которых следует производить настройку:
   ![image](https://github.com/user-attachments/assets/99119bec-c107-4ddb-b681-d339df9e9f98)

   Он же, измененный, после удаления пользователя admin:    
   ![image](https://github.com/user-attachments/assets/2dfd76bb-5eeb-4739-8e02-17996f5406b0)
   ![image](https://github.com/user-attachments/assets/1ea8c4b5-d514-4154-a95a-aa87d331d68e)

5. Для настройки устройств был создан Ansible плейбук chr_playbook.yaml:
   ![image](https://github.com/user-attachments/assets/454efb98-7352-44d9-a796-e72b421a2d6a)
   ![image](https://github.com/user-attachments/assets/1f360edd-73e0-4ca4-b28c-2c39788e4a38)
   
6. Выполнение плейбука с помощью команды    
   ```ansible-playbook -i inventory.yaml configure_chr.yml```
   ![image](https://github.com/user-attachments/assets/34243124-26d6-45da-adf4-a8c830c69362)
   ![image](https://github.com/user-attachments/assets/b2d93d35-addc-4370-9f60-fab6c42925d8)

7. Вывод конфига устройств:
   ```
   TASK [Print OSPF topology]         *********************************************************************************************************************************************************
   ok: [chr1] => {
       "ospf_neighbors.stdout_lines": [
            [
                "Flags: V - virtual; D - dynamic"
            ]
        ]
    }
    ok: [chr2] => {
        "ospf_neighbors.stdout_lines": [
            [
                "Flags: V - virtual; D - dynamic"
            ]
        ]
     }

    TASK [Print full config] 
    ***********************************************************************************************************************************************************
    ok: [chr1] => {    
        "full_config.stdout_lines": [    
            [    
                "# 2024-11-24 16:17:31 by RouterOS 7.16.1",    
                "# software id = ",    
                "#",    
                "/interface wireguard",    
                "add listen-port=13231 mtu=1420 name=wg0",    
                "/interface list",    
                "add name=WAN",    
                "add name=LAN",    
                "/ip pool",    
                "add name=vpn ranges=192.168.89.2-192.168.89.255",    
                "/ppp profile",    
                "set *FFFFFFFE local-address=192.168.89.1 remote-address=vpn",    
                "/routing ospf instance",    
                "add disabled=no name=default router-id=1.1.1.1",    
                "/routing ospf area",    
                "add disabled=no instance=default name=backbone",    
                "/interface l2tp-server server",    
                "set enabled=yes use-ipsec=yes",    
                "/interface list member",    
                "add interface=ether1 list=WAN",    
                "/interface wireguard peers",    
                "add allowed-address=10.14.14.0/24,    224.0.0.5/32,    1.1.1.1/32 endpoint-address=\\",    
                "    192.168.111.54 endpoint-port=13231 interface=wg0 name=peer \\",    
                "    persistent-keepalive=25s public-key=\\",    
                "    \"HAihpVWrqkMngJS+jrJVR+BDHda44aM0dzguYkXusRs=\"",    
                "/ip address",    
                "add address=10.14.14.2/24 interface=wg0 network=10.14.14.0",    
                "add address=1.1.1.1 interface=lo network=1.1.1.1",    
                "/ip dhcp-client",    
                "add interface=ether1",    
                "/ip dns",    
                "set allow-remote-requests=yes servers=8.8.8.8,    8.8.4.4",    
                "/ip firewall filter",    
                "add action=accept chain=input protocol=icmp",    
                "add action=accept chain=input protocol=ospf",    
                "add action=accept chain=output protocol=ospf",    
                "add action=accept chain=input protocol=ospf",    
                "add action=accept chain=output protocol=ospf",    
                "add action=accept chain=input protocol=ospf",    
                "add action=accept chain=output protocol=ospf",    
                "/ip firewall nat",    
                "add action=masquerade chain=srcnat out-interface=ether1",    
                "add action=masquerade chain=srcnat comment=\"masq. vpn traffic\" src-address=\\",    
                "    192.168.89.0/24",    
                "/ip route",    
                "add disabled=yes dst-address=0.0.0.0/0 gateway=192.168.110.1",    
                "/ppp secret",    
                "add name=vpn",    
                "/routing ospf interface-template",    
                "add area=backbone dead-interval=20s disabled=no hello-interval=5s interfaces=\\",    
                "    wg0 type=ptp",    
                "/system logging",    
                "add topics=ospf",    
                "add topics=ospf",    
                "/system note",    
                "set show-at-login=no",    
                "/system ntp client",    
                "set enabled=yes",    
                "/system ntp client servers",    
                "add address=194.190.168.1"
            ]    
        ]     
    }    
    ok: [chr2] => {    
        "full_config.stdout_lines": [    
            [    
                "# 2024-11-24 16:17:41 by RouterOS 7.16.1",    
                "# software id = ",    
                "#",    
                "/disk",    
                "set sata1 media-interface=none media-sharing=no",    
                "/interface ethernet",    
                "set [ find default-name=ether1 ] name=ether3",    
               "/interface wireguard",    
                "add listen-port=13231 mtu=1420 name=wg1",    
                "/interface list",    
                "add name=WAN",    
                "add name=LAN",    
                "/ip pool",    
                "add name=vpn ranges=192.168.89.2-192.168.89.255",    
                "/ppp profile",    
                "set *FFFFFFFE local-address=192.168.89.1 remote-address=vpn",    
                "/routing ospf instance",    
                "add disabled=no name=default router-id=2.2.2.2",    
                "/routing ospf area",    
                "add disabled=no instance=default name=backbone",    
                "/ipv6 settings",    
                "set max-neighbor-entries=16384",    
                "/interface l2tp-server server",    
                "set enabled=yes use-ipsec=yes",    
                "/interface list member",    
                "add interface=*2 list=WAN",    
                "/interface wireguard peers",    
                "add allowed-address=10.14.14.0/24,    224.0.0.5/32,    2.2.2.2/32 endpoint-address=\\",    
                "    192.168.111.54 endpoint-port=13231 interface=wg1 name=peer \\",    
                "    persistent-keepalive=25s public-key=\\",    
                "    \"HAihpVWrqkMngJS+jrJVR+BDHda44aM0dzguYkXusRs=\"",    
                 "/ip address",    
                "add address=10.14.14.3/24 interface=wg1 network=10.14.14.0",    
                "add address=192.168.110.90/23 interface=ether3 network=192.168.110.0",    
                "add address=2.2.2.2 interface=lo network=2.2.2.2",    
                "/ip dhcp-client",    
                "# Interface not active",    
                "add interface=*2",    
                "/ip dns",    
                "set allow-remote-requests=yes servers=8.8.8.8,    8.8.4.4",    
                "/ip firewall filter",    
                "add action=accept chain=input protocol=icmp",    
                "add action=accept chain=input protocol=ospf",    
                "add action=accept chain=output protocol=ospf",    
                "add action=accept chain=input protocol=ospf",    
                "add action=accept chain=output protocol=ospf",    
                "/ip firewall nat",    
                "# no interface",    
                "add action=masquerade chain=srcnat out-interface=*2",    
                "add action=masquerade chain=srcnat comment=\"masq. vpn traffic\" src-address=\\",    
                "    192.168.89.0/24",    
                "/ip route",    
                "add dst-address=10.14.14.0/24 gateway=wg1",    
                "add dst-address=10.14.14.0/24 gateway=wg1",    
                "/ppp secret",    
                "add name=vpn",    
                "/routing ospf interface-template",    
                "add area=backbone dead-interval=20s disabled=no hello-interval=5s interfaces=\\",    
                "    wg1 type=ptp",    
                "/system logging",    
                "add topics=ospf",    
                "add topics=ospf",    
                "/system note",    
                "set show-at-login=no",    
                "/system ntp client",    
                "set enabled=yes",    
                "/system ntp client servers",    
                "add address=194.190.168.1"     
            ]     
        ]     
    }    
   ```
   
8. Надо сверить, что полученные конфигурации корректны:
   ![image](https://github.com/user-attachments/assets/20e4ed8c-33df-4652-8eed-c9098f972f75)
   ![image](https://github.com/user-attachments/assets/ceeeffd5-c936-4c5b-b6e1-6162a24ffd0e)
   ![image](https://github.com/user-attachments/assets/6ee827f4-7886-4fbf-b2dd-eccd41e9b4a4)

   



Результаты лабораторной работы

