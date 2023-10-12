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

PC n° 1 : 10.0.0.10/24    ipv6 fd35:255d:c32a::10/64   
PC n° 2 : 10.0.0.11/24    ipv6 fda3:7a3b:6111::11/64      

![image](https://github.com/techerbeatrice/Utiliser_GNU_Linux_comme_routeur_IP/assets/138071140/3a5ce3c0-ebfc-46ca-8c8e-04ecdd2c9f84)

![image](https://github.com/techerbeatrice/Utiliser_GNU_Linux_comme_routeur_IP/assets/138071140/1392d376-0da2-4660-9d26-827b91819c39)

![image](https://github.com/techerbeatrice/Utiliser_GNU_Linux_comme_routeur_IP/assets/138071140/e1818d42-0529-47a1-bcbe-e2d3cd8a2b6f)

![image](https://github.com/techerbeatrice/Utiliser_GNU_Linux_comme_routeur_IP/assets/138071140/8ce5141e-dd78-493e-b034-68d72bc14d22)

![image](https://github.com/techerbeatrice/Utiliser_GNU_Linux_comme_routeur_IP/assets/138071140/e6285877-3a73-498e-9564-8a6c4c54c439)

![image](https://github.com/techerbeatrice/Utiliser_GNU_Linux_comme_routeur_IP/assets/138071140/14f0c9b9-b526-41ee-a032-70c0fdcd5fa7)

