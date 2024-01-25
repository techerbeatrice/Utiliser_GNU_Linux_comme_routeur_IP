# Utiliser GNU/Linux comme routeur IP


Commence par construire un réseau physique avec 2 machines et fait communiquer ces 2 machines avec IPv4 et IPv6.

Pour pouvoir utiliser des adresses privées pour ces machines, notamment pour IPv6, il te faut un identifiant de site : 40 bits tirés au sort.
Pour rappel, tu peux utiliser Unique Local IPv6 Generator.

|  routeur1 interface 1|10.0.0.1/24 |fdd3:9430:138e::1/64  |pour activer le routage, édite le fichier /etc/sysctl.conf --> net.ipv4.ip_forward = 1 --> tape la commande sysctl -p /etc/sysctl.conf  |   |
|---|---|---|---|---|
| pc1 ubuntu | 10.0.0.10/24  |fdd3:9430:138e::10/64   | ip address add **10.0.0.10/24 dev enp0s3**  |ip route add default via **10.0.0.1** --> ip route add default via **fdd3:9430:138e::1** --> ping **192.168.0.250/24** --> ping **fdd3:9430:138e:192::250**|
|  pc2 windows | 10.0.0.11/24  |fdd3:9430:138e::11/64  | ipconfig **10.0.0.11 255.2555.255.0**  |netsh interface ipv4 add route 0.0.0.0/0 **10.0.0.1** --> netsh interface ipv6 add route **::0 fdd3:9430:138e::1** --> ping **192.168.0.250/24** --> ping **fdd3:9430:138e:192::250** |
| **routeur1 inferface 2** |**192.168.0.250/24**  |**fdd3:9430:138e:192::250/64**  |   |   |   |
| **routeur2 inferface 1** |**192.168.0.250/24**  |**fdd3:9430:138e:192::250/64**  |   |   |   |
| pc3 ubuntu | 10.0.0.10/24  |fdd3:9430:138e::10/64   | ip address add **10.0.0.10/24 dev enp0s3**  |ip route add default via **10.0.0.1** --> ip route add default via **fdd3:9430:138e::1** --> ping **192.168.0.250/24** --> ping **fdd3:9430:138e:192::250**|
| **routeur2 inferface 2** |**192.168.0.250/24**  |**fdd3:9430:138e:192::250/64**  |   |   |   |
| **routeur3 inferface 1** |**192.168.0.250/24**  |**fdd3:9430:138e:192::250/64**  |   |   |   |
| **routeur3 inferface 2** |**192.168.0.250/24**  |**fdd3:9430:138e:192::250/64**  |   |   |   |
|  pc4 windows | 10.0.2.13/24  |fdd3:9430:138e::13/64  | ipconfig **10.0.2.13 255.2555.255.0**  |netsh interface ipv4 add route 0.0.0.0/0 **10.0.2.1** --> netsh interface ipv6 add route **::0 fdd3:9430:138e::1** --> ping **192.168.0.250/24** --> ping **fdd3:9430:138e:192::250** |
______

**Configuration ip dynamique sur le PC n°1**   

![image](https://github.com/techerbeatrice/Utiliser_GNU_Linux_comme_routeur_IP/assets/138071140/2a4473ab-1a0b-4bfa-8d51-9188b6b3e03f)
![image](https://github.com/techerbeatrice/Utiliser_GNU_Linux_comme_routeur_IP/assets/138071140/c2b89aa1-857c-4280-99d0-fe9d712acadf)

**Configuration ip statique sur le PC ubuntu n°1**    

#Fichier /etc/network/interfaces  
auto enp0s3    
#IPv4 configuration   
iface enp0s3 inet static address 10.0.0.10/24     
#IPv6 configuration   
iface enp0s3 inet6 static address fdd3:9430:138e::10/64     

____

**Configuration statique de la machine 10**  

#Fichier /etc/network/interfaces   
auto enp0s3   
iface enp0s3 inet static   
	address 10.0.0.10   
	netmask 255.255.255.0   
	gateway 10.0.0.1   

iface enp0s3 inet6 static   
	address fdd3:9430:138e::10   
	netmask 64   
	gateway fdd3:9430:138e::1    
