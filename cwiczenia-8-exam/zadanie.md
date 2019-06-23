Zadanie 1
-

![zadanie 1](zadanie-1.svg)

1. Zaprojektuj oraz przygotuj prototyp rozwiązania z wykorzystaniem oprogramowania ``VirtualBox`` lub podobnego. 
Zaproponuj rozwiązanie spełniające poniższe wymagania:
   * Usługodawca zapewnia domunikację z siecią internet poprzez interfejs ``eth0`` ``PC0``
   * Zapewnij komunikację z siecią internet na poziomie ``LAN1`` oraz ``LAN2``
   * Dokonaj takiego podziału sieci o adresie ``172.22.128.0/17`` aby w ``LAN1`` można było zaadresować ``500`` adresów natomiast w LAN2 ``5000`` adresów    
   * Przygotuj dokumentację powyższej architektury w formie graficznej w programie ``DIA``
   
#### LAN1:
 
 Maska: 255.255.254.0/23 <br>
 Adres podsieci: 172.22.160.0
 
#### LAN2:

 Maska: 255.255.224.0/19<br>
 Adres podsieci: 172.22.128.0
 
#### PC0:
 
 eth0: Połączenie z internetem<br>
 eth1: 172.22.128.1/19<br>
 eth2: 172.22.160.1/23<br>
 
#### PC1:

 eth0: 172.22.160.2/23<br>
 
#### PC2:
 
 eth0: 172.22.128.2/19<br>
 
#### usage:
 
 1. ``ip addr add`` xxx.xxx.xxx.xxx/xx ``dev`` nazwa interfejsu - set adresy <br> 
>PC0 - 172.22.160.1/23 i 172.22.128.1/19 <br> 
>PC1 - 172.22.160.2/23<br> 
>PC2 - 172.22.128.2/19<br>
 
2. echo 1 > /proc/sys/net/ipv4/ip_forward - set przekazywanie adresów ( ip forwarding )
 
3. ``pico /etc/resolv.conf`` - set default DNS ( 8.8.8.8 )
 
4. ``ip route add default via`` adres_interfejsu_pc0 - set brama domyślna dla hostów
>PC1 - 172.22.160.1/23
>PC2 - 172.22.128.1/19

5. ``iptables -t nat -A POSTROUTING -o ``nazwa_interfejsu ``-j MASQUERADE`` - pozwoli na udostępnienie internetu PC1 i PC2
