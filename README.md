
# Projet-IT_Magasin_Généraliste

Projet personnel de conception et paramétrage d'un réseau destiné à un usage de magasin généraliste

Le fichier Packet Tracer est mis à disposition dans le repository




## Contexte

La chaîne de magasins Toutadibal vient de construire un nouveau magasin et souhaite mettre en place son réseau informatique, celui-ci sera composé :

D'une partie Front Office, comportant :
- 4 caisses enregistreuses manuelles
- 3 caisses enregitreuses automatiques
- 1 borne Wifi pour les clients
- 3 caméras de sécurité

D'une partie Back Office, comportant :
- 1 poste destiné au manager du magasin
- 1 poste destiné à la gestion de l'inventaire
- 1 imprimante
- 1 caméra de sécurtié

Le personnel du magasin disposent d'appareils de téléphonie mobiles fournis, des téléphones IPs ne sont donc pas nécessaires.

Il est impératif que les consignes de sécurité suivantes soient respéctées :
- Seul le manager peut avoir accés au systéme de surveillance du magasin
- Seuls les utilisateurs du Back Office peuvent avoir accés à l'imprimante
- Les clients pourront avoir libre accés à Internet via la borne Wifi, mais ne pourront en aucun cas avoir accés au réseau interne du magasin




## Topologie

Voici la topologie finale de l'infrastructure :

<img width="1004" height="648" alt="image" src="https://github.com/user-attachments/assets/5baa94df-0d1d-4f80-8fc8-028570c62d11" />



## Plan d'adressage

- @ WAN : 203.0.115.5

- VLAN 10 : CAISSES	 192.168.10.0 /24
- VLAN 20 : CAISSES_AUTO 192.168.20.0 /24
- VLAN 30 : BACK_OFFICE	 192.168.30.0 /24
- VLAN 40 : COPIEURS	 192.168.40.0 /24
- VLAN 50 : GUEST_WIFI	 192.168.50.0 /24
- VLAN 60 : CAMERAS	 192.168.60.0 /24
- VLAN 99 : ADMIN	 192.168.99.0 /24
- VLAN 999 : BLACKHOLE
- PTP DST-SW1/EDGE-RTR : 10.0.0.0 /30
- ISP/SERVEUR DE PAIEMENT : 172.16.10.0 /24

- Nom de domaine : toutadibal.local





## Sécurité

- Seuls les VLANs 10,20,30,40,50,60,99 sont autorisés sur les liens trunks
- ACL étendue COPIEURS sur DST-SW1 :
    - Restreint le traffic accédant au SVI VLAN 40 aux utilisateurs du VLAN 30 (BACK OFFICE) et VLAN 99 (ADMINS) seulement
- ACL standard SSH sur les équipements réseaux :
    - Autorise l'accéss aux lignes vty 0 15 seulement au VLAN 99 (admins)
- ACL étendue ACCES_CAMERAS sur DST-SW1 :
    - Autorise l'accés aux caméras de sécurité aux utilisateurs du VLAN 30 (BACK OFFICE) et VLAN 99 (ADMINS) seulement
- VLAN par défaut 999 (BLACKHOLE) sur les switchs distributions et access
- BLACKHOLE VLAN 999 pour les interfaces inutilisées
- Configuration du service DHCP Snooping sur les switchs de la couche Access
- Portfast et BPDUGuard activé sur les ports access de la couche Access
## Mots de passe

- Mode privilégié : Admin123!
- SSH : Ssh123!
- VTP : Vtp123!

