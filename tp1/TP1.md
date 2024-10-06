# TP1 : Les premiers pas de bébé B1

<br />

## I. Récolte d'informations

<br />

**🌞 Adresses IP de ta machine**

Affiche l'adresse IP que ta machine a sur sa carte réseau WiFi :

    PS C:\Users\sheef> ipconfig

        Adresse IPv4. . . . . . . . . . . . . .: 10.33.77.159

Affiche l'adresse IP que ta machine a sur sa carte réseau ethernet :

<br />

**🌞 Si t'as un accès internet normal, d'autres infos sont forcément dispos...**

Affiche l'adresse IP de la passerelle du réseau local :

    PS C:\Users\sheef> ipconfig

        Passerelle par défaut. . . . . . . . . : 10.33.79.254

Affiche l'adresse IP du serveur DNS que connaît ton PC :

    PS C:\Users\sheef> ipconfig /all

        Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8

Affiche l'adresse IP du serveur DHCP que connaît ton PC :

    PS C:\Users\sheef> ipconfig /all

        Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254

<br />

**🌟 BONUS : Détermine s'il y a un pare-feu actif sur ta machine**

    PS C:\Users\sheef>  Get-NetFirewallProfile | ft Name,Enabled

        Name    Enabled
        ----    -------
        Domain     True
        Private    True
        Public     True

    
    PS C:\Windows\system32> New-NetFirewallRule -DisplayName "Autoriser le Bureau à distance (RDP)" -Group "Bureau à distance" -Profile Domain -Enabled True -Action Allow

        Name                          : {ba5099ab-0508-4c08-9348-6be9e9d4429e}
        DisplayName                   : Autoriser le Bureau à distance (RDP)
        Description                   :
        DisplayGroup                  : Bureau à distance
        Group                         : Bureau à distance
        Enabled                       : True
        Profile                       : Domain
        Platform                      : {}
        Direction                     : Inbound
        Action                        : Allow
        EdgeTraversalPolicy           : Block
        LooseSourceMapping            : False
        LocalOnlyMapping              : False
        Owner                         :
        PrimaryStatus                 : OK
        Status                        : La règle a été analysée à partir de la banque. (65536)
        EnforcementStatus             : NotApplicable
        PolicyStoreSource             : PersistentStore
        PolicyStoreSourceType         : Local
        RemoteDynamicKeywordAddresses : {}
        PolicyAppId                   :

<br />

## II. Utiliser le réseau

<br />

**🌞 Envoie un ping vers...**

<br />

Fais un ping vers ta propre adresse IP :

    PS C:\Users\sheef> ping 10.33.77.159

        Envoi d’une requête 'Ping'  10.33.77.159 avec 32 octets de données :
        Réponse de 10.33.77.159 : octets=32 temps<1ms TTL=128
        Réponse de 10.33.77.159 : octets=32 temps<1ms TTL=128
        Réponse de 10.33.77.159 : octets=32 temps<1ms TTL=128
        Réponse de 10.33.77.159 : octets=32 temps<1ms TTL=128

        Statistiques Ping pour 10.33.77.159:
        Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
        Durée approximative des boucles en millisecondes :
        Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms

Vers l'adresse IP 127.0.0.1 :

    PS C:\Users\sheef> ping 127.0.0.1

        Envoi d’une requête 'Ping'  127.0.0.1 avec 32 octets de données :
        Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
        Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
        Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
        Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128

        Statistiques Ping pour 127.0.0.1:
        Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
        Durée approximative des boucles en millisecondes :
        Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms

<br />

**🌞 On continue avec ping. Envoie un ping vers...**

ta passerelle :

    PS C:\Users\sheef> ping 10.33.79.254

        Délai d’attente de la demande dépassé.
        Délai d’attente de la demande dépassé.
        Délai d’attente de la demande dépassé.
        Délai d’attente de la demande dépassé.

        Statistiques Ping pour 10.33.79.254:
        Paquets : envoyés = 4, reçus = 0, perdus = 4 (perte 100%),

un(e) pote sur le réseau :

    PS C:\Users\sheef> ping 10.33.76.110

        Envoi d’une requête 'Ping'  10.33.76.110 avec 32 octets de données :
        Réponse de 10.33.76.110 : octets=32 temps=6 ms TTL=128
        Réponse de 10.33.76.110 : octets=32 temps=5 ms TTL=128
        Réponse de 10.33.76.110 : octets=32 temps=5 ms TTL=128
        Réponse de 10.33.76.110 : octets=32 temps=6 ms TTL=128

        Statistiques Ping pour 10.33.76.110:
        Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
        Durée approximative des boucles en millisecondes :
        Minimum = 5ms, Maximum = 6ms, Moyenne = 5ms

un site internet :

    PS C:\Users\sheef> ping www.google.fr

        Envoi d’une requête 'ping' sur www.google.fr [172.217.20.195] avec 32 octets de données :
        Réponse de 172.217.20.195 : octets=32 temps=17 ms TTL=116
        Réponse de 172.217.20.195 : octets=32 temps=17 ms TTL=116
        Réponse de 172.217.20.195 : octets=32 temps=23 ms TTL=116
        Réponse de 172.217.20.195 : octets=32 temps=16 ms TTL=116

        Statistiques Ping pour 172.217.20.195:
        Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
        Durée approximative des boucles en millisecondes :
        Minimum = 16ms, Maximum = 23ms, Moyenne = 18ms

<br />

**🌞 Faire une requête DNS à la main**

    PS C:\Users\sheef> nslookup www.thinkerview.com

        Serveur :   dns.google
        Address:  8.8.8.8

        Réponse ne faisant pas autorité :
        Nom :    www.thinkerview.com
        Addresses:  2a06:98c1:3120::7
          2a06:98c1:3121::7
          188.114.96.7
          188.114.97.7


    PS C:\Users\sheef> nslookup www.wikileaks.org

        Serveur :   dns.google
        Address:  8.8.8.8

        Réponse ne faisant pas autorité :
        Nom :    wikileaks.org
        Addresses:  51.159.197.136
          80.81.248.21
        Aliases:  www.wikileaks.org

    
    PS C:\Users\sheef> nslookup www.torproject.org

        Serveur :   dns.google
        Address:  8.8.8.8

        Réponse ne faisant pas autorité :
        Nom :    www.torproject.org
        Addresses:  2a01:4f8:fff0:4f:266:37ff:feae:3bbc
          2620:7:6002:0:466:39ff:fe7f:1826
          2a01:4f9:c010:19eb::1
          2a01:4f8:fff0:4f:266:37ff:fe2c:5d19
          2620:7:6002:0:466:39ff:fe32:e3dd
          95.216.163.36
          116.202.120.165
          204.8.99.146
          204.8.99.144
          116.202.120.166

<br />

## III. Sniffer le réseau

<br />

**🌞 J'attends dans le dépôt git de rendu un fichier ping.pcap**

[lien vers ma capture](./ping.pcapng)

<br />

**🌞 Livrez un deuxième fichier : dns.pcap**

[lien vers ma capture](./dns.pcapng)

<br />

## IV. Network scanning et adresses IP

<br />

**🌞 Effectue un scan du réseau auquel tu es connecté**

    PS C:\Users\sheef> nmap -sn -PR 192.168.56.0/24

<br />

**🌞 Changer d'adresse IP**

    PS C:\Users\sheef> ipconfig

        Adresse IPv4. . . . . . . . . . . . . .: 192.168.0.74