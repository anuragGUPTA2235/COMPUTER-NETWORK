![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/ade9b385-9f9e-4e82-8ac1-0f59dcf872e3)
## Features
http </br>
dns</br>
dhcp</br>
vlan</br>
intervlan routing through router on a stick</br>
repeater</br>
wireless access point</br>
wireless routers</br>
3G/4G cell tower connectivity</br>
internet access with modem throught phoneline</br>
multi router connection through serial</br>
public and private ip addresses</br>
different class of ips used
<BR/>
## Building Concepts
![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/fe620d18-e531-4059-84f7-e58022e90d13)
```bash
\\router dhcp server ip : 11.0.0.9
en
conf t
interface gigabitethernet0/0/0
ip address 10.0.0.1 255.255.255.0
ip helper-address 11.0.0.9
interface gigabitethernet0/0/1
ip address 11.0.0.1 255.255.255.0
ip helper-address 11.0.0.9
```
![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/306c3814-c8d9-481c-bd2a-b514724db48f)
![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/fdbdb8a0-8649-4795-8a8e-f2a07d072f15)
```bash
//ethernet1
en
conf t
interface fastethernet0/1
ip address 10.0.0.1 255.255.255.0
switchport mode access
switchport access vlan 20
exit
exit
write memory
//ethernet2
en
conf t
interface fastethernet0/2
ip address 10.0.0.2 255.255.255.0
switchport mode access
switchport access vlan 30
exit
exit
write memory
//ethernet3
en
conf t
interface fastethernet0/3
ip address 10.0.0.3 255.255.255.0
switchport mode access
switchport access vlan 40
exit
exit
write memory
```
![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/32a0c200-6f45-4e4c-9472-58705a607b98)
```bash
//// switch 1
//ethernet1
en
conf t
interface fastethernet0/1
ip address 10.0.0.1 255.255.255.0
switchport mode access
switchport access vlan 20
exit
exit
write memory
//ethernet2
en
conf t
interface fastethernet0/2
ip address 10.0.0.2 255.255.255.0
switchport mode access
switchport access vlan 30
exit
exit
write memory
//ethernet3
en
conf t
interface fastethernet0/3
ip address 10.0.0.3 255.255.255.0
switchport mode access
switchport access vlan 40
exit
exit
write memory
//// switch 2
//ethernet1
en
conf t
interface fastethernet0/1
ip address 11.0.0.1 255.255.255.0
switchport mode access
switchport access vlan 40
exit
exit
write memory
\\\\\ trunk port switch 1
\\ethernet4
en
conf t
interface fastethernet0/4
ip address 10.0.0.4 255.255.255.0
switchport mode trunk
switchport trunk vlan allowed 20,30,40
exit
exit
write memory
\\\\\ trunk port switch 2
\\ethernet2
en
conf t
interface fastethernet0/2
ip address 11.0.0.2 255.255.255.0
switchport mode trunk
switchport trunk vlan allowed 20,30,40
exit
exit
write memory
```
![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/3a441944-955c-4937-be1a-d589f76a3e2e)
```bash
//// switch 1
//ethernet1
en
conf t
interface fastethernet0/1
switchport mode access
switchport access vlan 20
exit
exit
write memory
//ethernet2
en
conf t
interface fastethernet0/2
switchport mode access
switchport access vlan 30
exit
exit
write memory
//ethernet3
en
conf t
interface fastethernet0/3
switchport mode access
switchport access vlan 40
exit
exit
write memory
// trunk port ethernet 4
interface fastethernet0/4
switchport mode trunk
switchport trunk vlan allowed 20,30,40
exit
exit
write memory 
// router on a stick -- inter-vlan routing
en
conf t
interface gigabitethernet0/0/0
ip address 9.0.0.1 255.255.255.0
interface gigabitethernet0/0/0.20
ip address 10.0.0.1 255.255.255.0
interface gigabitethernet0/0/0.30
ip address 11.0.0.1 255.255.255.0
interface gigabitethernet0/0/0.40
ip address 12.0.0.1 255.255.255.0
give gateway to pc connected in vlan20 as 10.0.0.1
give gateway to pc connected in vlan30 as 11.0.0.1
give gateway to pc connected in vlan40 as 12.0.0.1
now you can ping between the three vlans
```
![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/ee4ef788-0a7b-4df8-b73a-71b925634b0f)
![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/8ea77cfa-d274-486d-817b-2db987962e37)
![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/f78959b2-11ca-467f-8449-f04c55cd9b51)
![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/411a4aa4-3edf-4bf4-8a68-ae9ae7a22d53)
![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/d13a778a-8552-4cda-888a-f21312b040bb)
## Interior Gateway Protocols:
### Open Shortest Path Protocol
![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/168d3fff-c44a-405d-9ebb-1f8bb6220611)
```bash
/// router1
en
conf t
interface gigabitethernet0/0/0
ip address 10.0.0.1 255.255.255.0
interface gigabitethernet0/0/1
ip address 13.0.0.1 255.255.255.0
exit
exit
write memory
/// router2
en
conf t
interface gigabitethernet0/0/0
ip address 13.0.0.2 255.255.255.0
interface gigabitethernet0/0/1
ip address 15.0.0.1 255.255.255.0
exit
exit
write memory
/// router1
en
conf t
router ospf 1
network 10.0.0.0 0.0.0.255 area 0
network 13.0.0.0 0.0.0.255 area 0
exit
exit
write memory
/// router2
en
conf t
router ospf 1
network 13.0.0.0 0.0.0.255 area 0
network 15.0.0.0 0.0.0.255 area 0
exit
exit
write memory
```
![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/dd35082e-ca4d-4206-94a2-35a2efecfe82)
```bash
\\\ neighbour table
show ip ospf neighbor
```
![ospf2](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/b6b34ac6-9f8d-44e9-b5a2-0e9fcbabf668)
```bash
\\\ topology table link state database
\\\ every entry is link state advertisement
show ip ospf database
```
![ospf3](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/fb6d6da8-c2a6-48c2-94a4-97764b27b78a)
```bash
\\\ routing table
show ip route
```
### Routing Information Protocol
![image](https://github.com/anuragGUPTA2235/COMPUTER-NETWORK/assets/161227082/381c2de0-b9b6-4dab-a9e9-cf3fe671ce15)
```bash
// router 1
en
conf t
interface gigabitethernet0/0/0
ip address 10.0.0.1 255.255.255.0
interface gigabitethernet0/0/1
ip address 13.0.0.1 255.255.255.0
exit
exit
write memory
// router 2
en
conf t
interface gigabitethernet0/0/0
ip address 13.0.0.2 255.255.255.0
interface gigabitethernet0/0/1
ip address 15.0.0.1 255.255.255.0
exit
exit
write memory
// router 1
en
conf t
router rip
network 10.0.0.0
network 13.0.0.0
exit
exit
write memory
// router 2
en
conf t
router rip
network 13.0.0.0
network 15.0.0.0
exit
exit
write memory
```















