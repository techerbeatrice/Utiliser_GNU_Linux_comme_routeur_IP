# Utiliser GNU/Linux comme routeur IP

**Exercice - étape 1**   

Commence par construire un réseau physique avec 2 machines et fait communiquer ces 2 machines avec IPv4 et IPv6.

Pour pouvoir utiliser des adresses privées pour ces machines, notamment pour IPv6, il te faut un identifiant de site : 40 bits tirés au sort.
Pour rappel, tu peux utiliser Unique Local IPv6 Generator.

Dans la suite de la quête, on utilise l'identifiant : d3:9430:138e, donc le préfixe fdd3:9430:138e.
Mais pour respecter le protocole, tu dois bien avoir ton propre identifiant aléatoire pour ta mise en œuvre !

Configure la première machine (10) avec : 10.0.0.10/24 et fd<ton id de site>::10/64 (pour l'exemple : fdd3:9430:138e::10/64) et la deuxième machine (11) avec : 10.0.0.11/24 et fd<ton id de site>::11/64

Test, par exemple avec ping, qu'il est possible de joindre la première machine à partir de la deuxième et vice-versa.

____

PC n° 1 : 10.0.0.10/24    ipv6 fdd3:9430:138e::10/64   
PC n° 2 : 10.0.0.11/24    ipv6 fdd3:9430:138e::11/64      

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

______

**Exercice - étape 2**   

On ajoute maintenant un routeur (r0) à ce réseau.   

Ce routeur dispose de 2 interfaces réseaux.   
La première est sur le même réseau que les machines 10 et 11 avec la configuration suivante :   

10.0.0.1/24 et fdd3:9430:138e::1/64   
La seconde est sur un second réseau ethernet qui accueillera d'autres routeurs plus tard. Sa configuration est :   

192.168.0.250/24 et fdd3:9430:192::250/64   
En plus de configurer les interfaces réseaux de cette machine, il faut aussi activer le routage IPv4 et IPv6 au niveau du noyau comme indiqué dans l'article suivant.    

____

**Configuration dynamique de la table de routage sur la machine 10 ou 11**    

$ sudo ip route add default via 10.0.0.1   
$ ping 192.168.0.250     
PING 192.168.0.250 (192.168.0.250) 56(84) bytes of data.   
64 bytes from 192.168.0.250: icmp_seq=1 ttl=64 time=1.71 msip    

$ sudo ip route add default via fdd3:9430:138e::1   
$ ping fdd3:9430:138e:192::250   
PING fdd3:9430:138e:192::250(fdd3:9430:138e:192::250) 56 data bytes   
64 bytes from fdd3:9430:138e:192::250: icmp_seq=1 ttl=64 time=0.618 ms   


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
