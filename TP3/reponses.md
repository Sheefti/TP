# TP3 : 32°13'34"N 95°03'27"W

<br />

## I. ARP basics

<br />

**☀️ Avant de continuer...**

    PS C:\Users\sheef> ipconfig /all

        Adresse physique . . . . . . . . . . . : 0A-00-27-00-00-0C

<br />

**☀️ Affichez votre table ARP**

    PS C:\Users\sheef> arp -a

        Interface : 192.168.56.1 --- 0xc
        Adresse Internet      Adresse physique      Type
        192.168.56.255        ff-ff-ff-ff-ff-ff     statique
        224.0.0.22            01-00-5e-00-00-16     statique
        224.0.0.251           01-00-5e-00-00-fb     statique
        224.0.0.252           01-00-5e-00-00-fc     statique
        239.255.255.250       01-00-5e-7f-ff-fa     statique
        255.255.255.255       ff-ff-ff-ff-ff-ff     statique

        Interface : 10.33.77.159 --- 0x14
        Adresse Internet      Adresse physique      Type
        10.33.65.63           44-af-28-c3-6a-9f     dynamique
        10.33.73.77           98-8d-46-c4-fa-e5     dynamique
        10.33.76.110          28-c5-d2-ea-30-53     dynamique
        10.33.77.29           58-cd-c9-22-43-fd     dynamique
        10.33.77.160          c8-94-02-f8-ab-97     dynamique
        10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
        10.33.79.255          ff-ff-ff-ff-ff-ff     statique
        224.0.0.22            01-00-5e-00-00-16     statique
        224.0.0.251           01-00-5e-00-00-fb     statique
        224.0.0.252           01-00-5e-00-00-fc     statique
        239.255.255.250       01-00-5e-7f-ff-fa     statique
        255.255.255.255       ff-ff-ff-ff-ff-ff     statique

<br />

**☀️ Déterminez l'adresse MAC de la passerelle du réseau de l'école**

    PS C:\Users\sheef> arp -a

          10.33.79.254          7c-5a-1c-d3-d8-76     dynamique

adresse MAC : 7c-5a-1c-d3-d8-76

<br />

**☀️ Supprimez la ligne qui concerne la passerelle**

    PS C:\Windows\system32> arp -d 10.33.79.254 

<br />

**☀️ Prouvez que vous avez supprimé la ligne dans la table ARP**

    PS C:\Windows\system32> arp -d 10.33.79.254 ; arp -a

        Interface : 192.168.56.1 --- 0xc
        Adresse Internet      Adresse physique      Type
        192.168.56.255        ff-ff-ff-ff-ff-ff     statique
        224.0.0.22            01-00-5e-00-00-16     statique
        224.0.0.251           01-00-5e-00-00-fb     statique
        224.0.0.252           01-00-5e-00-00-fc     statique
        239.255.255.250       01-00-5e-7f-ff-fa     statique
        255.255.255.255       ff-ff-ff-ff-ff-ff     statique

        Interface : 10.33.77.159 --- 0x14
        Adresse Internet      Adresse physique      Type
        10.33.65.63           44-af-28-c3-6a-9f     dynamique
        10.33.73.77           98-8d-46-c4-fa-e5     dynamique
        10.33.76.110          28-c5-d2-ea-30-53     dynamique
        10.33.77.29           58-cd-c9-22-43-fd     dynamique
        10.33.77.160          c8-94-02-f8-ab-97     dynamique
        10.33.79.255          ff-ff-ff-ff-ff-ff     statique
        224.0.0.22            01-00-5e-00-00-16     statique
        224.0.0.251           01-00-5e-00-00-fb     statique
        224.0.0.252           01-00-5e-00-00-fc     statique
        239.255.255.250       01-00-5e-7f-ff-fa     statique
        255.255.255.255       ff-ff-ff-ff-ff-ff     statique

<br />

**☀️ Wireshark**

[lien vers ma capture](arp1.pcapng)

<br />

## II. ARP dans un réseau local
## 1. Basics

<br />

**☀️ Déterminer**

    PS C:\Users\sheef> ipconfig /all
    
        192.168.231.2


    PS C:\Windows\system32> arp -a

        e6-0f-c1-06-f5-1d

<br />

**☀️ DIY**


    PS C:\Users\sheef> ipconfig

        Adresse IPv4. . . . . . . . . . . . . .: 192.168.231.219(préféré)


    nouvelle ip : 192.168.231.25 

    PS C:\Users\sheef> ipconfig /all

        Carte réseau sans fil Wi-Fi :

        Suffixe DNS propre à la connexion. . . :
        Description. . . . . . . . . . . . . . : MediaTek Wi-Fi 6E MT7902 Wireless LAN Card
        Adresse physique . . . . . . . . . . . : F8-54-F6-BA-C5-1A
        DHCP activé. . . . . . . . . . . . . . : Non
        Configuration automatique activée. . . : Oui
        Adresse IPv4. . . . . . . . . . . . . .: 192.168.231.25(préféré)
        Masque de sous-réseau. . . . . . . . . : 255.255.255.0
        Passerelle par défaut. . . . . . . . . : 192.168.231.2
        Serveurs DNS. . .  . . . . . . . . . . : 192.168.231.2
        NetBIOS sur Tcpip. . . . . . . . . . . : Activé

<br />

**☀️ Pingz !**

    PS C:\Users\sheef> ping 192.168.231.56

        Statistiques Ping pour 192.168.231.56:
            Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
        Durée approximative des boucles en millisecondes :
            Minimum = 5ms, Maximum = 17ms, Moyenne = 9ms

<br />

## 2. ARP

<br />

**☀️ Affichez votre table ARP !**

    PS C:\Windows\system32> arp -a

        Interface : 192.168.231.25 --- 0x14
        Adresse Internet      Adresse physique      Type
        192.168.231.2         e6-0f-c1-06-f5-1d     dynamique
        192.168.231.56        28-c5-d2-ea-30-53     dynamique

<br />

**☀️ Capture arp2.pcap**

[lien vers ma capture](arp2.pcapng)

