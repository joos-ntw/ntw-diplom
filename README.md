# Дипломная работа по курсу «Сетевой инженер»
# Островский Евгений

* [Цель дипломной работы](#цель-дипломной-работы)
* [Чек-лист готовности к выполнению  дипломной работы](#чек-лист-готовности-к-выполнению-дипломной-работы)
* [Задание](#задание)
* [Этапы выполнения](#этапы-выполнения) 
* [Тестирование](#тестирование) 
* [Правила приема дипломной работы](#правила-приема-дипломной-работы)
* [Критерии оценки дипломной работы](#критерии-оценки-дипломной-работы)


### Цель дипломной работы
 

В результате выполнения этого задания вы научитесь настраивать хорошо масштабируемую отказоустойчивую и защищённую сеть, выделяя для каждого пользовательского сервиса уникальные права и пропускную полосу. Также вы научитесь объединять разрозненные филиальные сети компании в одну единую. Для удобства администрирования вы научитесь интегрировать инструменты централизованной аутентификации и логирования в настроенную вами сеть. 


1. Настроить отказоустойчивую связку RSTP+HSRP на уровне доступ-ядро.
2. Подготовить безопасное централизованное назначение сетевых настроек для оконечных устройств.
3. Организовать централизованный беспроводной гостевой доступ к сети интернет.
4. Организовать отказоустойчивую маршрутизацию в сети компании.
5. Организовать отказоустойчивый доступ к сети интернет по протоколу BGP.
6. Развернуть сервис VoIP внутри компании.
7. Настроить сервисы централизованной аутентификации, синхронизации времени и логирования сетевых устройств.
8. Настроить сеть компании полностью "под ключ".


### Чек-лист готовности к выполнению дипломной работы

Для выполнения работ потребуется:

1. Понимание протоколов маршрутизации eBGP, OSPF.
2. Понимание предсказуемного поведения протоколов RSTP, HSRP, LAG.
3. Знание протоколов безопасного подключения к уровню доступа (vlan, trunk, portfast, bpduguard, dhcp-snooping)
4. Умение настраивать туннельный протокол GRE.
5. Умение настраивать Qos для голосового трафика внутри GRE.
6. Знание aaa, tacacs+, NTP, syslog.
7. Умение настраивать устройства беспроводной сети: AP, WLC.
8. Умение настраивать внутреннюю voip-телефонию.
9. Знание особенностей настройки межсетевого экранирования на Cisco ASA.
10. Умение настраивать static NAT, PAT overload. 

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения дипломной работы

1. Packet Tracer 8.2.2
   [Шаблон топологии PT 8.0.0](https://github.com/netology-code/ntw-diplom/blob/main/ntw_topology_8.0.0.pkt)
   [Шаблон топологии PT 8.2.1](https://github.com/netology-code/ntw-diplom/blob/main/ntw_topology_8.2.1.pkt)
   [Шаблон топологии PT 8.2.2](https://github.com/netology-code/ntw-diplom/blob/main/ntw_topology_8.2.2.pkt)
2. [Таблица распределения подсетей и адресов](https://github.com/netology-code/ntw-diplom/blob/main/ip-address-table.xlsx)
------

## Задание

Нужно настроить отказоустойчивую, безопасную, масштабируемую сеть и запустить на ней пользовательские сервисы. 

### Этапы выполнения

1) Соберите топологию сети в Cisco Packet tracer. 
      Модели сетевого оборудования: 
      * border-router - 1941, 
      * fw - ASA 5506-x, 
      * ядро - 3560-24, 
      * доступ - 2960-24, 
      * wlan - WLC-2504, 
      * 3702i AP, 
      * internet - switch 3650, 
      * VOIP-server - router 2811, 
      * ip-phone 7960. 

      Используйте за основу [шаблон топологии](https://github.com/netology-code/ntw-diplom#%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D1%8B-%D0%B8-%D0%B4%D0%BE%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5-%D0%BC%D0%B0%D1%82%D0%B5%D1%80%D0%B8%D0%B0%D0%BB%D1%8B-%D0%BA%D0%BE%D1%82%D0%BE%D1%80%D1%8B%D0%B5-%D0%BF%D1%80%D0%B8%D0%B3%D0%BE%D0%B4%D1%8F%D1%82%D1%81%D1%8F-%D0%B4%D0%BB%D1%8F-%D0%B2%D1%8B%D0%BF%D0%BE%D0%BB%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B4%D0%B8%D0%BF%D0%BB%D0%BE%D0%BC%D0%BD%D0%BE%D0%B9-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%8B), в котором уже есть оборудование, настройки которого изменять нельзя.

      ![image](https://user-images.githubusercontent.com/5977962/192236499-941224d0-4694-4c74-8cb1-95a068e99fda.png)

## [Топология сети](https://github.com/joos-ntw/ntw-diplom/blob/main/%D0%A2%D0%B5%D1%81%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5.md)

2) Заполните [таблицу распределения подсетей и адресов](https://github.com/netology-code/ntw-diplom/blob/main/ip-address-table.xlsx) (по примеру коммутатора "internet"). 

      Нужно учёсть возможность добавления пяти новых коммутаторов доступа в ЦО, и открытия трёх новых филиалов:

      ![image](https://user-images.githubusercontent.com/5977962/199594168-8d9f3a98-5eed-4438-9b83-53f9b9cd9393.png)

## [Таблица ip-address-table](https://github.com/joos-ntw/ntw-diplom/blob/main/configs/ip-address-table.xlsx)

3) Настройте на коммутаторах доступа порты для подключения пользовательских устройств и аплинки. Также на пользовательских портах коммутатора следует настроить: 
     * port-security на 3 адреса, 
     * dhcp-snooping, 
     * portfast, 
     * RSTP.
     
  ![image](https://user-images.githubusercontent.com/5977962/192258720-b8f713d3-e42a-4af4-87ed-36efc8629c71.png)

Сделал настройки
```
 switchport trunk allowed vlan 100,200,300,400,500
 ip dhcp snooping trust

 spanning-tree mode rapid-pvst
 spanning-tree portfast default

 switchport mode access
 switchport access vlan X
 switchport port-security
 switchport port-security maximum 3
 switchport port-security violation restrict
```
4) Настройте на коммутаторах ядра: 
     * vlan, 
     * LAG, 
     * RSTP, 
     * SVI,
     * dhcp-relay 
     * HSRP для всех vlan.  
  
   На этом шаге проверьте работу stp, lag. 
       
  ![image](https://user-images.githubusercontent.com/5977962/193780747-d0c64050-94db-499c-8d9e-9f3b7a06f5de.png)

  ![192258850-47edbb83-3118-4f1b-b735-dd280b103df6](https://user-images.githubusercontent.com/85602495/194490766-5d5ef8e8-7fe6-4ed0-a8a5-643a8de66ce5.png)

```
core1#sh spanning-tree summary 
Switch is in rapid-pvst mode
Root bridge for: VLAN0100 VLAN0200 VLAN0300 VLAN0400 VLAN0500
Extended system ID           is enabled
Portfast Default             is disabled
PortFast BPDU Guard Default  is disabled
Portfast BPDU Filter Default is disabled
Loopguard Default            is disabled
EtherChannel misconfig guard is disabled
UplinkFast                   is disabled
BackboneFast                 is disabled
Configured Pathcost method used is short

Name                   Blocking Listening Learning Forwarding STP Active
---------------------- -------- --------- -------- ---------- ----------
VLAN0001                     4         0        0          3          7
VLAN0100                     6         0        0          1          7
VLAN0200                     6         0        0          1          7
VLAN0300                     6         0        0          1          7
VLAN0400                     6         0        0          1          7
VLAN0500                     6         0        0          1          7

---------------------- -------- --------- -------- ---------- ----------
6 vlans                     34         0        0          8         42


core1#show etherchannel port-channel
                Channel-group listing:
                ----------------------

Group: 1
----------
                Port-channels in the group:
                ---------------------------

Port-channel: Po1    (Primary Aggregator)
------------

Age of the Port-channel   = 00d:00h:-17m:-25s
Logical slot/port   = 2/1       Number of ports = 2
GC                  = 0x00000000      HotStandBy port = null
Port state          = Port-channel 
Protocol            =   LACP
Port Security       = Disabled

Ports in the Port-channel:

Index   Load   Port     EC state        No of bits
------+------+------+------------------+-----------
  0     00     Fa0/23   Active             0
  0     00     Fa0/22   Active             0
Time since last port bundled:    00d:00h:-17m:-25s    Fa0/22
```

5) Настройте сервисы для распределения сетевых настроек для пользовательских устройств. Так как сервер находится в отдельной сети, на SVI настраивается helper. По окончанию настроек dhcp-сервер должен раздать настройки PC, телефонам и принтерам, с любого хоста ЦО должен быть доступен любой другой хост.  
  ![image](https://user-images.githubusercontent.com/5977962/192258899-0278a6e5-815b-458d-bed0-bbab3d21603f.png)

```
interface Vlan100
 description MGMT
 ip address 10.10.10.3 255.255.255.128
 ip helper-address 10.10.10.10
 standby version 2
 standby 100 ip 10.10.10.1
 standby 100 priority 110
 standby 100 preempt
```

6) Настройте сервис БЛВС. Точки доступа должны подключаться к контроллеру, который сообщит им настройки по capwap. Подключите ноутбук к ТД, проверьте связность сети.
![image](https://user-images.githubusercontent.com/5977962/192258971-afec76f9-8e71-45e5-af8a-7a6debcf767c.png)

![51](https://github.com/joos-ntw/ntw-diplom/raw/main/img/51.png)

7) На коммутаторах ядра запустите протокол маршрутизации ospf. Он должен анонсировать все внутренние сети в зоне 1.
![image](https://user-images.githubusercontent.com/5977962/192259147-f4fbe92b-440f-41ba-a54e-036e14eaf0d8.png)

```
router ospf 1
 log-adjacency-changes
 area 1 nssa no-summary
 network 10.10.10.0 0.0.0.127 area 1
 network 10.10.20.0 0.0.0.255 area 1
 network 10.10.30.0 0.0.0.255 area 1
 network 10.10.40.0 0.0.0.255 area 1
 network 10.10.50.0 0.0.0.127 area 1
 network 10.10.1.8 0.0.0.3 area 1
```

8) На каждом межсетевом экране настройте адресацию и три зоны: inside, outside, DMZ.  
   
   Правила фильтрации:
   * из inside доступ свободный во все зоны
   * из outside в inside и DMZ доступ разрешен для траффика от приватных адресов
   * из DMZ разрешен доступ только в outside на публичные адреса

![image](https://user-images.githubusercontent.com/5977962/192261102-8b1924bf-0a03-44a7-96b8-8fb0e4e3e2e1.png)

Настроил, поправил security-level где необходимо
```
interface GigabitEthernet1/1
 nameif DMZ
 security-level 50
 ip address 10.10.5.1 255.255.255.128
!
interface GigabitEthernet1/2
 nameif inside
 security-level 100
 ip address 10.10.1.13 255.255.255.252
!
interface GigabitEthernet1/3
 nameif outside
 security-level 0
 ip address 10.10.1.6 255.255.255.252
 
```

9) На Cisco ASA настройте протокол ospf. МСЭ должен принимать и анонсировать все сети в зоне 1.  
   Настройте web-сервер, подключенный в DMZ зону одной из ASA.  

   На этом шаге проверьте:  
   * все ли сети получены
   * все ли сети анонсируются на коммутаторы ядра
   * есть ли доступ к web-серверу и с него

```
router ospf 1
 log-adjacency-changes
 area 1 nssa no-summary
 network 10.10.1.4 255.255.255.252 area 1
 network 10.10.1.12 255.255.255.252 area 1
 network 10.10.5.0 255.255.255.128 area 1
```

10) Настройте пограничные маршрутизаторы. Настройте адресацию и проверьте сетевую связность внутри ЛВС и доступность шлюза провайдера. 

```
interface GigabitEthernet0/0
 ip address 172.1.0.2 255.255.255.252
```
```
Router#ping 10.10.1.10

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.10.1.10, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 0/0/0 ms

Router#ping 172.1.0.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 172.1.0.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 0/0/0 ms
```
11) Настройте маршрутизацию ospf: 
 * интерфейсы в сторону ASA в зоне 1 
 * между собой в зоне 0   
 
   Настройте анонс маршрута 0.0.0.0/0 во внутреннюю сеть с разными метриками для резервирования подключения. Другие маршруты с бордеров во внутреннюю сеть не должны анонсироваться. Проверьте получение и анонс маршрутов.  
  ![image](https://user-images.githubusercontent.com/5977962/193406159-cd3286ac-3eaa-4ea1-90b2-1530c8de7ce5.png)

```
router ospf 1
 log-adjacency-changes
 area 1 nssa no-summary
 network 10.10.1.0 0.0.0.3 area 1
 network 10.10.1.100 0.0.0.0 area 1
 network 10.10.1.20 0.0.0.3 area 0
```

12) Настройте ebgp-сессии с оборудованием провайдера. Проверьте получение и анонс маршрутов. 
![image](https://user-images.githubusercontent.com/5977962/193406083-3f31ed36-3f14-4406-8b73-9d7d3d9c8c65.png)

```
router bgp 65200
 bgp log-neighbor-changes
 no synchronization
 neighbor 172.1.0.1 remote-as 65100
 network 172.1.0.0 mask 255.255.255.252
```

13) Настройте правила NAT,PAT на пограничных маршрутизаторах.

```
interface GigabitEthernet0/0
 ip address 172.1.0.2 255.255.255.252
 ip nat outside
!
interface GigabitEthernet0/1
 ip address 10.10.1.1 255.255.255.252
 ip nat inside

ip nat inside source list 10 interface GigabitEthernet0/0 overload
access-list 10 permit 10.10.20.0 0.0.0.255
access-list 10 permit 10.10.30.0 0.0.0.255
```

14) Настройте маршрутизатор филиала: адресацию, статический маршрут до роутеров ЦО через провайдера. Проверьте связность с внешними интерфейсами бордеров ЦО.  
![image](https://user-images.githubusercontent.com/85602495/194488837-7e68a8a5-be09-4937-8e9c-7f7c0810bac5.png)

```
interface GigabitEthernet0/0
 ip address 172.3.0.2 255.255.255.252
 ip nat outside
ip nat inside source list 10 interface GigabitEthernet0/0 overload
ip route 172.2.0.0 255.255.255.252 172.3.0.1 
ip route 172.1.0.0 255.255.255.252 172.3.0.1
ip route 0.0.0.0 0.0.0.0 172.3.0.1 
```
```
Router#ping 172.1.0.2

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 172.1.0.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 0/0/0 ms

Router#ping 172.2.0.2

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 172.2.0.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 0/0/0 ms
```

15) На маршрутизаторе филиала настройте Tunnel-интерфейсы gre до бордеров ЦО. А так же протокол ospf для получения и анонса внутренних сетей. Туннельные интерфейсы  в зоне 2.  
  ![image](https://user-images.githubusercontent.com/5977962/193405773-e0dc77ea-b506-4fad-9700-11e270a8b418.png)

```
interface Tunnel13
 ip address 10.10.1.29 255.255.255.252
 mtu 1476
 tunnel source GigabitEthernet0/0
 tunnel destination 172.3.0.2

 router ospf 1
 network 10.10.1.28 0.0.0.3 area 2


interface Tunnel23
 ip address 10.10.1.33 255.255.255.252
 mtu 1476
 tunnel source GigabitEthernet0/0
 tunnel destination 172.3.0.2

router ospf 1
 network 10.10.1.32 0.0.0.3 area 2


interface Tunnel31
 ip address 10.10.1.30 255.255.255.252
 mtu 1476
 tunnel source GigabitEthernet0/0
 tunnel destination 172.1.0.2

interface Tunnel32
 ip address 10.10.1.34 255.255.255.252
 mtu 1476
 tunnel source GigabitEthernet0/0
 tunnel destination 172.2.0.2

router ospf 1
 log-adjacency-changes
 network 10.10.1.28 0.0.0.3 area 2
 network 10.10.1.32 0.0.0.3 area 2
 network 10.10.11.0 0.0.0.255 area 2
 network 10.10.21.0 0.0.0.255 area 2
 network 10.10.41.0 0.0.0.255 area 2
 network 10.10.51.0 0.0.0.255 area 2
 network 10.10.31.0 0.0.0.255 area 2
```

16) Настройте коммутатор доступа филиала для подключения к сети ip-телефона, ПК и точки доступа. На маршрутизаторе настройте helper для централизованного получения сетевых настроек оконечными устройствами. 
![image](https://user-images.githubusercontent.com/85602495/194488342-09e1a8db-8e12-4d8e-9939-57b045cc70ab.png)

```
interface GigabitEthernet0/1.201
 description USER
 encapsulation dot1Q 201
 ip address 10.10.21.1 255.255.255.128
 ip helper-address 10.10.10.10
 ip access-group VLAN201 in
!
interface GigabitEthernet0/1.301
 description USER
 encapsulation dot1Q 301
 ip address 10.10.31.1 255.255.255.128
 ip helper-address 10.10.10.8
 ip access-group VLAN301 in
```

17) Настройте БЛВС ТД филиала, подключить к ней ноутбук. Проверьте сетевую связность.

![52](https://github.com/joos-ntw/ntw-diplom/raw/main/img/52.png)

18) Настройте на АСО интерфейсы для управления. Настройте на них аутентификацию по tacacs+, синхронизацию часов(NTP) с сервером и отправку логов по syslog(на ASA настройка aaa и syslog не требуется, достаточно локальной учётной записи). 

![181](https://github.com/joos-ntw/ntw-diplom/raw/main/img/181.png)

![182](https://github.com/joos-ntw/ntw-diplom/raw/main/img/182.png)

![183](https://github.com/joos-ntw/ntw-diplom/raw/main/img/183.png)


19) Настройте ip-телефоны, проверьте дозвон.

![191](https://github.com/joos-ntw/ntw-diplom/raw/main/img/62.png)

Кратко опишите, чем чреват выбор протокола GRE для объединения сети ЦО и филиала в 15 пункте. Какие более безопасные альтернативы можно предложить без потери функциональности?

Критические недостатки GRE:
- Нет шифрования — весь трафик передается в открытом виде
- Нет аутентификации — возможна подмена туннелей
- Уязвимость к атакам — MITM, инъекции пакетов
- Статическая конфигурация — сложность масштабирования

Альтернативы
- IPsec
- Другой VPN который можно настроить на оборудовании


### [Тестирование](https://github.com/joos-ntw/ntw-diplom/blob/main/%D0%A2%D0%B5%D1%81%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5.md)

1) Проверка STP, HSRP. Роль Root bridge и HSRP-active на одном устройстве. Команды: show spanning-tree, show standby на этом устройстве.
2) Проверка маршрутизации на коммутаторах ядра. Show ip route. Должен присутствовать маршрут по-умолчанию и маршруты до интерфейсов ASA и бордеров.
3) Проверка LAG на коммутаторах ядра show etherchannel summary.
4) Маршрутизация на бордерах sh ip route. В таблице маршрутизации должны присутствовать bgp-маршруты от провайдера, ospf-маршруты до внутренних подсетей ЦО и филиала.
5) Туннель CAPWAP на БЛВС ТД в статусе Connected, с ноутбуков есть связь с 8.8.8.8.
6) Телефонные аппараты зарегестрированы на VoIP сервере, прозвон с одного на другой работает.
7) На все сетевые устройства можно попасть по учётной записи tacacs+ сервера.
8) Время на устройствах синхронизировано. Show ntp status.
9) С 8.8.8.8 есть доступ к web-серверу в DMZ. Обратный доступ тоже есть. Проверять доступ необходимо браузером.
10) Отключение одного из каналов связи не приводит к потере доступа в интернет с пользовательских ПК(ping до сервера 8.8.8.8). 
11) Выход из строя одного из коммутаторов ядра, межсетевого экрана или бордер роутера не приводит к потере доступа в интернет с пользовательских ПК(ping до сервера 8.8.8.8). Потеря доступа к web-серверу извне доспускается.
12) Ноутбуки не имеют доступа к внутренним сетям компании(ping svi users, mgmt, printer).
13) Устройства филиала имеют доступ только к внутренним сетям компании, не имеют выхода в интернет.

ПРИМЕЧАНИЯ:
В связи с особенностью эмулятора Packet Tracer, часто бывает так, что для того, чтобы тест заработал, нужно перезагрузить устройства.
Для корректной работы statefull инспекции протокола icmp необходимо удалить стандартные настройки инспекции на Cisco ASA(class-map, policy-map, service policy) и создать собственные под другими названиями.

------

### Правила приема дипломной работы

В качестве выполненной работы прикрепите в личном кабинете файлы, содержащие следующую информацию:
* Пояснительную записку, которая содержит таблицы и описания к решениям, указанным на всех этапах выполнения работ. Обоснование предполагает короткое описание (1-3 предложения) выбранного технического решения, которое должно ответить на вопрос, почему вы выбрали именно это решение, а не иное. 
* Собранную топологию в PacketTracer в виде. pkt файла.
* Конфигурационные файлы с оборудования.
* Результаты тестирования, проведенного на шаге "Тестирование", в виде отдельного текстового файла с вложенными в него скриншотами и трассировками.

### Критерии оценки проекта

1. Зачёт:
   - Топология построена корректно.
   - Адреса и подсети распределены с учётом размера сети и возможного масштабирования. 
   - Все тесты пройдены успешно.
   
   Допускается не более 3 ошибок в тестах и двух ошибок в выделении подсетей.
   
2. Незачёт:

   - Ошибки в выделении адресов, подсетей и масок, более трёх тестов не пройдено.

