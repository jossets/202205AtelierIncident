# Atelier Gestion des Incidents



## Cyberattaque au CHU de Rouen


Info: 1 min

https://www.youtube.com/watch?v=TqojSAQvCAs

Europe 1: 2 min

https://www.youtube.com/watch?v=OnoIzhajFvw

Directeur Hopital: 7 min 

https://www.youtube.com/watch?v=tJro-tSV0qs

Le Monde

https://www.lemonde.fr/pixels/article/2019/11/18/frappe-par-une-cyberattaque-massive-le-chu-de-rouen-force-de-tourner-sans-ordinateurs_6019650_4408996.html

Echanges:
- Que s'est-il passé ?
- Comment l'hopital a-t-il réagit ?
- Quelles sont les conséquences pour les médecins, les patients ?
- Quels messages veut faire passer le DSI ?

Mots clefs :
```
3 axes: 
- Reorg DSI
- Infra technique (dont Securité)
- Application :   Parc logiciel modernisé (windows XP ?)
  
  
Vendredi soir (pourquoi ?)

Pb de cx (attaque des vpn ?)
Cyber attaque 

Mobilisation d'une équipe (qui ?)
jours/nuit 
Remettre en place (quel process ?)


ANNSI (Les pompiers en cas d'attaque !!!)
  contact, aide 
  ANNSI Cyber 
  SI   

Procédure dégradées (obligation, heureusement ?)
  Procédures en place 
  
Dimanche
1 semaine toutes les applis 

AD 
Poste de travail 
Droits strictes Privileges administrateur 
18 000 comptes utilisateurs soignants, chercheurs et administratifs

Authent par carte certificat+code, login+password SSO 

Données clients 
Entrepot de données de santé  
General Data Protection Regulation (GDPR) – Official Legal Text


IoT 
Maitriser l'usage 
```

## Cyberattaque d'une PME 

 
Envoyé spécial: 30 min, regarder jusqu'à 3,56 min

https://www.youtube.com/watch?v=JrFoFBNfv7A

Echanges:
- Quelles différences avec le cas de l'hopital ?
- Quel conséquence pour la PME ?
- La question ce n'est pas : est-ce que ça va arriver ? C'est quand ? Et qu'est ce qu'on fait ?


## Etre prêts: 

- Avoir anticipé le pire 

- Gérer l'incident en temps réel, continuer de fonctionner
  
- Plan de reprise d'activité, remettre dans les applis ce qui a été fait à la main 

- Analyse à froid, comprendre, éviter que ça recommence, aller au tribunal avec des preuves


Le role des process, des SOC, des formations 

L'ANNSI 

https://www.ssi.gouv.fr/


L'ENISA 

https://www.enisa.europa.eu






## Atelier Forensics 

Comprendre ce qui s'est passé pour éviter que ça se reproduise 



### Process forensic 


![Process Forensic](img/forensic_process.png)

- Data integrity: Ne rien faire qui puisse invalider une preuve au tribunal
- Audit trail: On trace TOUT ce qui est fait sur les preuves 
- Specialist support: Toute preuve doit être notifée à un expert.
- Appropriate training: Les intervenants doivent être formés aux process et ne pas improviser
- Legality: Le responsable doit s'assurer que tout est fait dansun cadre légal

![OSCAR](img/oscar.png)
- Obtain information
- Strategize
- Collect evidence
- Analyse
- Report



### Analyse de logs: Bruteforce sql d'une base de données 


- Système de collecte de logs centralisé
- Time stamps 
- CRC 

Se créer un compte sur root me. 
Etudier le chall: (https://www.root-me.org/fr/Challenges/Forensic/Analyse-de-logs-attaque-web)
- [datas/ch13.txt](datas/ch13.txt)

Une fois le mot de passe admin trouvé, l'accès au serveur se fait en utilisant le formulaire de login.


### Analyse d'une trace réseau: Exfiltration de données  


Une fois dans la place, le virus identifie les fichiers ayant de la valeur (.xls, .doc, password, compta,...), et les transmets par tunnels DNS, Ping, requètes Get/Post s'il n'y a pas de proxy avec authen,...

- [datas/exfiltration_dns.pcap](./datas/exfiltration_dns.pcap) Exfiltration DNS
- [datas/exfiltration_ping.pcap](./datas/exfiltration_dns.pcap) Exfiltration Ping
 
 
Outils
- wireshark 
- tshark 
- python 

Extraction de champs:
```
tshark -nr cap.pcap -Y "dns.flags.response == 0" -T fields -e dns.qry.name
```

Filtrer les protocoles 
```
tshark -r exfiltration.pcap |awk '{print $6}' |sort -u
```

Domaines de requete DNS 
```
tshark -r exfiltration.pcap -Y 'dns' -Tfields -e dns.qry.name |sort -u
```

Ping
```
tshark -r exfiltration.pcap -Y 'icmp'
```




### Analyse d'un disque 


Le logiciel va tenter d'effacer ses traces.
Effacement ou corruption des fichiers de logs. 
En effacement simple, laisse le contenu des fichiers sur le disque.
Il est parfois possible de les retrouver. 


- Faire une copie du disque avec une interface lecture seule [https://en.wikipedia.org/wiki/Forensic_disk_controller]
- Travailler sur une copie de la copie 

- Analyser le disque (format, partitions)
- Monter le disk en lecture seule 
- Analyser le contenu existant
- Chercher les fichiers effacés 

Images de disque
- [datas/usb1.img](./datas/usb1.img)
- [datas/usb2.img](./datas/usb2.img)

Outils:
- file 
- mount / umount 
- photorec  

References:
(https://tldp.org/LDP/sag/html/partitions.html)

 








