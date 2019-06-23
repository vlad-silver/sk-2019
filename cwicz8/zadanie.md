# 1. Podział sieci

a) Podział:

| sieć | adres | maska |
|:-----|:------|:------|
| LAN1 | 172.22.160.0 | 255.255.254.0/23 |
| LAN2 | 172.22.128.0 | 255.255.224.0/19 |
  
b) Wytłumaczenie:

Jeśli 500 urządzeń to maska musi być: ``255.255.254.0`` (/23)
  
Jeśli 5000 urządzeń to maska musi być: ``255.255.224.0`` (/19)

W innym przypadku nie wystarczy hostów.
``LAN1``: ``172.22.128.0``
``LAN2``: ``172.22.160.0`` ponieważ ``LAN1`` posiada 510 adresów (2^(32-2)-2).

--------------

# 2. Konfiguracja

PC0
---
|  interfejs   | adres  |
|:-------------| :------| 
| enp0s3 | 172.22.160.1/23  |
| enp0s8 | 172.22.128.1/19  |


PC1
---
|  interfejs   | adres  |
|:-------------| :------|
| enp0s3 | 172.22.160.2/23 | 


PC2
---
|  interfejs   | adres  |
|:-------------| :------| 
| enp0s3 | 172.22.128.2/19 |

--------------

**1. Ustawienie adresu ip:**  
``ip addr add`` + ip + ``dev`` + interfejs  

**2. IP forwarding w PC0:**  
``echo 1 > /proc/sys/net/ipv4/ip_forward``
**1. Ustawienie adresu ip:**  
``ip addr add`` + ip + ``dev`` + interfejs  

**2. IP forwarding w PC0:**  
``echo 1 > /proc/sys/net/ipv4/ip_forward``

**3. Dodanie trasy na PC1 i PC2:**  
``ip route add default via`` + adres IP PC0 dla danej karty

**4. DNS:**  
PC1 PC2
``/etc/resolv.conf``  

**5. Dodanie wpisu do tablicy routingu na PC0:**  
``iptables -t nat -A POSTROUTING -o`` + interfejs, który ma dostęp do internetu + ``-j MASQUERADE``





