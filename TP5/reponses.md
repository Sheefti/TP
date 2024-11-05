# TP5 : Un ptit LAN à nous

<br />

## I. Setup

<br />

**☀️ Uniquement avec des commandes, prouvez-que :**

    [tao@routeur ~]$ ip a
        inet 10.5.1.254/24 brd 10.5.1.255 scope global noprefixroute enp0s8

    tao@client1:~$ ip a
        inet 10.5.1.11/24 brd 10.5.1.255 scope global enp0s8
    
    tao@client2:~$ ip a
        inet 10.5.1.12/24 brd 10.5.1.255 scope global enp0s8

<br />

Routeur --> Client1 :

    [tao@routeur ~]$ ping 10.5.1.11
    PING 10.5.1.11 (10.5.1.11) 56(84) bytes of data.
    64 bytes from 10.5.1.11: icmp_seq=1 ttl=64 time=1.65 ms
    64 bytes from 10.5.1.11: icmp_seq=2 ttl=64 time=0.452 ms
    64 bytes from 10.5.1.11: icmp_seq=3 ttl=64 time=1.08 ms
    64 bytes from 10.5.1.11: icmp_seq=4 ttl=64 time=0.892 ms
    64 bytes from 10.5.1.11: icmp_seq=5 ttl=64 time=0.645 ms
    
    --- 10.5.1.11 ping statistics ---
    5 packets transmitted, 5 received, 0% packet loss, time 4020ms
    rtt min/avg/max/mdev = 0.452/0.945/1.654/0.414 ms

<br />

Routeur --> Client2 :

    [tao@routeur ~]$ ping 10.5.1.12
    PING 10.5.1.12 (10.5.1.12) 56(84) bytes of data.
    64 bytes from 10.5.1.12: icmp_seq=1 ttl=64 time=1.94 ms
    64 bytes from 10.5.1.12: icmp_seq=2 ttl=64 time=0.521 ms
    64 bytes from 10.5.1.12: icmp_seq=3 ttl=64 time=1.22 ms
    64 bytes from 10.5.1.12: icmp_seq=4 ttl=64 time=1.12 ms
    
    --- 10.5.1.12 ping statistics ---
    4 packets transmitted, 4 received, 0% packet loss, time 3008ms
    rtt min/avg/max/mdev = 0.521/1.200/1.944/0.505 ms

<br />

Client1 --> Client2 :

    tao@client1:~$ ping 10.5.1.12
    PING 10.5.1.12 (10.5.1.12) 56(84) bytes of data.
    64 bytes from 10.5.1.12: icmp_seq=1 ttl=64 time=3.82 ms
    64 bytes from 10.5.1.12: icmp_seq=2 ttl=64 time=0.515 ms
    64 bytes from 10.5.1.12: icmp_seq=3 ttl=64 time=1.03 ms
    64 bytes from 10.5.1.12: icmp_seq=4 ttl=64 time=1.90 ms
    64 bytes from 10.5.1.12: icmp_seq=5 ttl=64 time=0.697 ms

    --- 10.5.1.12 ping statistics ---
    5 packets transmitted, 5 received, 0% packet loss, time 4005ms
    rtt min/avg/max/mdev = 0.515/1.590/3.816/1.209 ms

<br />

Client1 --> Routeur :

    tao@client1:~$ ping 10.5.1.254
    PING 10.5.1.254 (10.5.1.254) 56(84) bytes of data.
    64 bytes from 10.5.1.254: icmp_seq=1 ttl=64 time=2.68 ms
    64 bytes from 10.5.1.254: icmp_seq=2 ttl=64 time=1.36 ms
    64 bytes from 10.5.1.254: icmp_seq=3 ttl=64 time=1.83 ms
    64 bytes from 10.5.1.254: icmp_seq=4 ttl=64 time=2.31 ms

    --- 10.5.1.254 ping statistics ---
    4 packets transmitted, 4 received, 0% packet loss, time 3005ms
    rtt min/avg/max/mdev = 1.358/2.043/2.677/0.497 ms

<br />

## II. Accès internet pour tous

### 1. Accès internet routeur

<br />

**☀ Déjà, prouvez que le routeur a un accès internet**

    [tao@routeur ~]$ ping www.ynov.com
    PING www.ynov.com (104.26.10.233) 56(84) bytes of data.
    64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=1 ttl=53 time=25.1 ms
    64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=2 ttl=53 time=33.3 ms
    64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=3 ttl=53 time=26.0 ms
    64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=4 ttl=53 time=25.8 ms

    --- www.ynov.com ping statistics ---
    4 packets transmitted, 4 received, 0% packet loss, time 3007ms
    rtt min/avg/max/mdev = 25.123/27.569/33.315/3.334 ms

<br />

**☀ Activez le routage**

    [tao@routeur ~]$ sudo firewall-cmd --add-masquerade --permanent
    success

    [tao@routeur ~]$ sudo firewall-cmd --reload
    success

<br />

### 2. Accès internet clients

<br />

**☀ Prouvez que les clients ont un accès internet**

    tao@client1:~$ ping www.ynov.com
    PING www.ynov.com (104.26.10.233) 56(84) bytes of data.
    64 bytes from 104.26.10.233: icmp_seq=1 ttl=52 time=26.9 ms
    64 bytes from 104.26.10.233: icmp_seq=2 ttl=52 time=28.2 ms
    64 bytes from 104.26.10.233: icmp_seq=3 ttl=52 time=26.2 ms
    64 bytes from 104.26.10.233: icmp_seq=4 ttl=52 time=27.6 ms
    
    --- www.ynov.com ping statistics ---
    5 packets transmitted, 4 received, 20% packet loss, time 4008ms
    rtt min/avg/max/mdev = 26.217/27.236/28.224/0.746 ms

    tao@client2:~$ ping www.ynov.com
    PING www.ynov.com (172.67.74.226) 56(84) bytes of data.
    64 bytes from 172.67.74.226: icmp_seq=1 ttl=52 time=26.3 ms
    64 bytes from 172.67.74.226: icmp_seq=2 ttl=52 time=27.1 ms
    64 bytes from 172.67.74.226: icmp_seq=3 ttl=52 time=26.2 ms
    64 bytes from 172.67.74.226: icmp_seq=4 ttl=52 time=26.4 ms

    --- www.ynov.com ping statistics ---
    4 packets transmitted, 4 received, 0% packet loss, time 3026ms
    rtt min/avg/max/mdev = 26.222/26.499/27.057/0.330 ms

<br />

**☀ Montrez-moi le contenu final du fichier de configuration de l'interface réseau**

    tao@client2:~$ cat /etc/netplan/01-netcfg.yaml
    network:
    version: 2
    renderer: networkd
    ethernets:
        enp0s8:
        dhcp4: no
        addresses: [10.5.1.12/24]
        gateway4: 10.5.1.254
        nameservers:
            addresses: [1.1.1.1]

<br />

## III. Serveur SSH

<br />

**☀ Sur routeur.tp5.b1, déterminer sur quel port écoute le serveur SSH**

    [tao@routeur ~]$ sudo ss -lnpt | grep 22
    LISTEN 0      128          0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=702,fd=3))
    LISTEN 0      128             [::]:22           [::]:*    users:(("sshd",pid=702,fd=4))

<br />

**☀ Sur routeur.tp5.b1, vérifier que ce port est bien ouvert**

    [tao@routeur ~]$ cat /etc/services | grep 22
    ssh             22/tcp                          # The Secure Shell (SSH) Protocol
    ssh             22/udp                          # The Secure Shell (SSH) Protocol

<br />

## IV. Serveur DHCP

### 3. Rendu attendu

### A. Installation et configuration du serveur DHCP

<br />

**☀ Installez et configurez un serveur DHCP sur la machine routeur.tp5.b1**

    [root@routeur tao]# dnf -y install dhcp-server


    [root@routeur tao]# vi /etc/dhcp/dhcpd.conf
    option domain-name-servers      1.1.1.1;
    subnet 10.5.1.0 netmask 255.255.255.0 {
        range dynamic-bootp 10.5.1.137 10.5.1.237;
        option routers 10.5.1.254;
    }

    [root@routeur tao]# systemctl enable --now dhcpd

    [root@routeur tao]# firewall-cmd --add-service=dhcp
    success

    [root@routeur tao]# firewall-cmd --runtime-to-permanent
    success

<br />

### B. Test avec un nouveau client

<br />

**☀ Créez une nouvelle machine client client3.tp5.b1**

    tao@client3:~$ ip a
         inet 10.5.1.137/24 metric 100 brd 10.5.1.255 scope global dynamic enp0s8

    tao@client3:~$ ping ynov.com
    PING ynov.com (104.26.10.233) 56(84) bytes of data.
    64 bytes from 104.26.10.233: icmp_seq=1 ttl=52 time=60.3 ms
    64 bytes from 104.26.10.233: icmp_seq=2 ttl=52 time=30.5 ms
    64 bytes from 104.26.10.233: icmp_seq=3 ttl=52 time=27.9 ms
    64 bytes from 104.26.10.233: icmp_seq=4 ttl=52 time=29.6 ms
    
    --- ynov.com ping statistics ---
    4 packets transmitted, 4 received, 0% packet loss, time 3109ms
    rtt min/avg/max/mdev = 27.884/37.075/60.300/13.441 ms

<br />

### C. Consulter le bail DHCP

<br />

☀ Consultez le bail DHCP qui a été créé pour notre client

    [root@routeur tao]# cd /var/lib/dhcpd/

    [root@routeur dhcpd]# cat dhcpd.leases
    lease 10.5.1.137 {
        starts 2 2024/11/05 01:27:13;
        ends 2 2024/11/05 13:27:13;
        cltt 2 2024/11/05 01:27:13;
        binding state active;
        next binding state free;
        rewind binding state free;
        hardware ethernet 08:00:27:45:55:eb;
        uid "\377\257\201\217}\000\002\000\000\253\021\231lL\227\0342K~";
    }

<br />

**☀ Confirmez qu'il s'agit bien de la bonne adresse MAC**

    tao@client3:~$ ip a
        link/ether 08:00:27:45:55:eb brd ff:ff:ff:ff:ff:ff

