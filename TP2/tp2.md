# TP2 : Hey yo tell a neighbor tell a friend

<br />

## 1. Quelques pings

<br />

**🌞 Prouvez que votre configuration est effective**

    PS C:\Users\sheef> Get-NetIPAddress -InterfaceAlias "Ethernet 3"

        IPAddress         : fe80::9756:7187:c692:fc64%15
        InterfaceIndex    : 15
        InterfaceAlias    : Ethernet 3
        AddressFamily     : IPv6
        Type              : Unicast
        PrefixLength      : 64
        PrefixOrigin      : WellKnown
        SuffixOrigin      : Link
        AddressState      : Preferred
        ValidLifetime     :
        PreferredLifetime :
        SkipAsSource      : False
        PolicyStore       : ActiveStore

        IPAddress         : 10.234.111.2
        InterfaceIndex    : 15
        InterfaceAlias    : Ethernet 3
        AddressFamily     : IPv4
        Type              : Unicast
        PrefixLength      : 24
        PrefixOrigin      : Manual
        SuffixOrigin      : Manual
        AddressState      : Preferred
        ValidLifetime     :
        PreferredLifetime :
        SkipAsSource      : False
        PolicyStore       : ActiveStore

<br />

**🌞 Tester que votre LAN + votre adressage IP est fonctionne**

    PS C:\Users\sheef> ping 10.234.111.1

        Statistiques Ping pour 10.234.111.1:
            Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
        Durée approximative des boucles en millisecondes :
            Minimum = 3ms, Maximum = 3ms, Moyenne = 3ms

<br />

**🌞 Capture de ping**

[lien vers ma capture](ping.pcapng)

<br />

## II. Utilisation des ports

<br />

**🌞 Sur le PC serveur**

    PS C:\Users\sheef\Desktop\COURS\netcat-win32-1.11\netcat-1.11> .\nc.exe

<br />

**🌞 Sur le PC serveur toujours**

    PS C:\Windows\system32> netstat -a -b -n

        TCP    0.0.0.0:9999           0.0.0.0:0              LISTENING
        [nc.exe]

<br />


**🌞 Echangez-vous des messages**

    PS C:\Users\sheef\Desktop\COURS\netcat-win32-1.11\netcat-1.11> .\nc.exe -l -p 9999
    oui
    sedlgdhg
    sedefùesf
    sf
    s


<br />

**🌞 Faites une capture Wireshark complète d'un échange**

serveur :

[lien vers ma capture](netcat1.pcapng)

<br />

# 🌞 Inversez les rôles

<br />

**🌞 Sur le PC client**

     PS C:\Users\sheef\Desktop\COURS\netcat-win32-1.11\netcat-1.11> .\nc.exe 10.234.111.1 875
    coucou
    mainon

<br />

**🌞 Utilisez une commande qui permet de voir la connexion en cours**

     TCP    10.234.111.2:50341     10.234.111.1:875       ESTABLISHED
     [nc.exe]

<br />

**🌞 Faites une capture Wireshark complète d'un échange**

client :

[lien vers ma capture](netcat2.pcapng)

<br />

## III. Analyse de vos applications usuelles

**1. Serveur web**

**🌞 Utilisez Wireshark pour capturer du trafic HTTP**

[lien vers ma capture](http.pcapng)

<br />

**🌞 Pour les 5 applications**

    PS C:\Windows\system32> netstat -a -b -n

[lien vers ma capture](discord.pcapng)

<br />

      TCP    192.168.0.101:21240    155.133.248.43:443     ESTABLISHED
    [steam.exe]

[lien vers ma capture](steam.pcapng)

<br />

      TCP    192.168.0.101:21319    95.100.200.81:443      ESTABLISHED
    [Deezer.exe]

[lien vers ma capture](deezer.pcapng)

<br />

      TCP    192.168.0.101:21435    20.112.54.230:443      ESTABLISHED
    [Solitaire.exe]

[lien vers ma capture](solitaire.pcapng)

<br />

      TCP    192.168.0.101:39553    74.125.206.188:5228    ESTABLISHED
    [opera.exe]

[lien vers ma capture](opera.pcapng)
