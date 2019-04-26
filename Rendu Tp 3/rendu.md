## RENDU TP3

## Manipulation de switches et de VLAN

**Pré-requis** :

- Configuration des clients 
	 - changement des adresses ip
	 - nom de domaine 

- Vérification des pings


**Configuration des VLANs**


- Configuration du switch 1 ( IOU1)
- Configuration du VLAN : 

    >     #conf t
    >     (config)# vlan "numero du VLAN"
    >     (config-vlan)# name client-network
    >     (config-vlan)# exit
    >     (config)# interface Ethernet 0/0
    >     (config-if)# switchport mode access
    >     (config-if)# switchport access vlan "numero du VLAN"


- Configuration du trunk : 

    > (config)# interface Ethernet 0/0 (config-if)# switchport trunk
    > encapsulation dot1q (config-if)# switchport mode trunk


- Vérification des pings : 

![enter image description here](https://github.com/Lilou444/CCNA2-2018/blob/master/Rendu%20Tp%203/captures/Capture2.png)


**Schema de la configuration **

![enter image description here](https://github.com/Lilou444/CCNA2-2018/blob/master/Rendu%20Tp%203/captures/Capture1.png)


## II. Manipulation simple de routeurs

**Toujours les mêmes pré-requis que le lab 1**


- Schéma de la configuration 
![enter image description here](https://github.com/Lilou444/CCNA2-2018/blob/master/Rendu%20Tp%203/captures/Capture3.png)


- Configuration du routeur Cisco 

    >  #conf t
    >     (config)# interface FastEthernet <NUMERO>
    >     (config-if)# ip address <IP> <MASK>
    >     (config-if)# no shut
    >     (config-if)# exit
    >     (config)# exit
    >     show ip int br


- Vérification des pings 

- Communication entre tous les équipements : comme vu au lab 1, le switch permet de relier plusieurs segments dans un réseau. Par conséquent il faudrait rajouter un switch.


## Mise en place d'OSPF

** Pré-requis **

Même démarche que le lab1 en rapport avec la table d'adressage du lab3

- Schéma 

![enter image description here](https://github.com/Lilou444/CCNA2-2018/blob/master/Rendu%20Tp%203/captures/Capture8.png)


- Exemple de deux routeurs après l'ajout d'ip statique 

    > R1#show ip int br Interface  IP-Address  OK? Method Status  Protocol
    > FastEthernet0/0  10.3.100.1  YES manual up  up FastEthernet1/0 
    > 10.3.100.22 YES manual up  up FastEthernet2/0  10.3.102.254  YES manual up  up


    > R4#show ip int br Interface  IP-Address  OK? Method Status  Protocol
    > FastEthernet0/0  10.3.100.10 YES manual up  up FastEthernet1/0 
    > 10.3.100.13 YES manual up  up FastEthernet2/0  10.3.101.254  YES manual up  up


- configuration du OSPF

//Passer en mode configuration

# conf t

>     Activation du OSPF
>     (config)# router ospf <ID OSPF>
>     (config-router)# router-id 1.1.1.1
>     (config-router)# network <NETWORK ADDRESS> <NETWORK MASK> area <ID AREA>
>     <=> (config-router)# network 10.6.100.0 0.0.0.3 area 0
>     //0.0.0.3 == 255.255.255.252
>     //0.0.0.255 == 255.255.255.0
>     
>     //Vérification de l'état OSPF
>     #show ip protocols
>     #show ip ospf interface
>     #show ip ospf neigh
>     #show ip ospf border-routers


- Vérification des pings 
![enter image description here](https://github.com/Lilou444/CCNA2-2018/blob/master/Rendu%20Tp%203/captures/Capture7.png)