# TP7 : On dit chiffrer pas crypter

<br />

## II. Serveur Web

### 1. HTTP

#### B. Configuration

<br />

    [root@routeur sitedefou.tp7.b1]# hostnamectl
    Static hostname: web.tp7.b1

(Je n'ai juste pas relancé le serveur web)

**🌞 Lister les ports en écoute sur la machine**

    [root@routeur sitedefou.tp7.b1]# sudo ss -lnpt
    State     Recv-Q    Send-Q         Local Address:Port         Peer Address:Port    Process
    LISTEN    0         511                  0.0.0.0:80                0.0.0.0:*        users:(("nginx",pid=11410,fd=6),("nginx",pid=11409,fd=6))
    LISTEN    0         511                     [::]:80                   [::]:*        users:(("nginx",pid=11410,fd=7),("nginx",pid=11409,fd=7))

<br />

**🌞 Ouvrir le port dans le firewall de la machine**

    [root@routeur sitedefou.tp7.b1]# sudo firewall-cmd --permanent --add-port=80/tcp
    success

    [root@routeur sitedefou.tp7.b1]# firewall-cmd --reload
    success

<br />

#### C. Tests client

<br />

**🌞 Vérifier que ça a pris effet**

    tao@client1:~$ ping sitedefou.tp7.b1
    PING sitedefou.tp7.b1 (10.7.1.11) 56(84) bytes of data.
    64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=1 ttl=64 time=3.08 ms
    64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=2 ttl=64 time=3.86 ms
    64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=3 ttl=64 time=1.25 ms
    64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=4 ttl=64 time=3.42 ms

    tao@client1:~$ curl http://sitedefou.tp7.b1
    meow !

<br />

#### D. Analyze

<br />

**🌞 Capture tcp_http.pcap**

[lien vers ma capture](tcp_http.pcapng)

<br />

**🌞 Voir la connexion établie**

    tao@client1:~$ ss -pnt
    tcp   ESTAB  0      0                                                 10.7.1.101:59290                                  10.7.1.11:http

<br />

### 2. On rajoute un S

#### A. Config

<br />

**🌞 Lister les ports en écoute sur la machine**

    [tao@web ~]$ ss -lnpt
    LISTEN   0        511              10.7.1.11:443             0.0.0.0:*       users:(("nginx",pid=1350,fd=6),("nginx",pid=1349,fd=6))

<br />

**🌞 Gérer le firewall**

    [tao@web ~]$ sudo firewall-cmd --permanent --add-port=443/tcp
    success

    [tao@web ~]$ sudo firewall-cmd --reload
    success

    [tao@web ~]$ sudo firewall-cmd --permanent --remove-port=80/tcp
    success

    [tao@web ~]$ sudo firewall-cmd --reload
    success

<br />

#### B. Test test test analyyyze

<br />

**🌞 Capture tcp_https.pcap**

[lien vers ma capture](tcp_https.pcapng)

<br />

## III. Serveur VPN

### 1. Install et conf Wireguard

<br />

**🌞 Prouvez que vous avez bien une nouvelle carte réseau wg0**

    [root@vpn tao]# ip a
    4: wg0: <POINTOPOINT,NOARP,UP,LOWER_UP> mtu 1420 qdisc noqueue state UNKNOWN group default qlen 1000
        link/none
        inet 10.7.200.1/24 scope global wg0
        valid_lft forever preferred_lft forever

<br />

**🌞 Déterminer sur quel port écoute Wireguard**

    [tao@vpn ~]$ ss -lnpu
    UNCONN  0       0              0.0.0.0:51820         0.0.0.0:*
    UNCONN  0       0                 [::]:51820            [::]:*

<br />

**🌞 Ouvrez ce port dans le firewall**

    [tao@vpn ~]$ sudo firewall-cmd --permanent --add-port=51820/tcp
    success

    [tao@vpn ~]$ sudo firewall-cmd --reload
    success

<br />

### 3. Proofs

<br />

**🌞 Ping ping ping !**

    tao@client1:~$ ping 10.7.200.1
    PING 10.7.200.1 (10.7.200.1) 56(84) bytes of data.
    
    --- 10.7.200.1 ping statistics ---
    4 packets transmitted, 0 received, 100% packet loss, time 3078ms

