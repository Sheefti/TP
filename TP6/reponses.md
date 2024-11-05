# TP6 : Des bo services dans des bo LANs

<br />

## I. Le setup

### 2. Marche à suivre

<br />

**☀ Prouvez que...**

    [root@dhcp tao]# ping www.ynov.com
    PING www.ynov.com (172.67.74.226) 56(84) bytes of data.
    64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=1 ttl=52 time=29.5 ms
    64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=2 ttl=52 time=32.3 ms
    64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=3 ttl=52 time=27.4 ms
    64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=4 ttl=52 time=29.6 ms
    
    --- www.ynov.com ping statistics ---
    4 packets transmitted, 4 received, 0% packet loss, time 3007ms
    rtt min/avg/max/mdev = 27.439/29.685/32.273/1.718 ms


    [tao@web ~]$ ping www.ynov.com
    PING www.ynov.com (104.26.10.233) 56(84) bytes of data.
    64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=1 ttl=52 time=29.0 ms
    64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=2 ttl=52 time=33.7 ms
    64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=3 ttl=52 time=27.6 ms
    64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=4 ttl=52 time=32.4 ms
    
    --- www.ynov.com ping statistics ---
    4 packets transmitted, 4 received, 0% packet loss, time 3012ms
    rtt min/avg/max/mdev = 27.582/30.668/33.740/2.486 ms


    [root@dhcp tao]# ping 10.6.2.11
    PING 10.6.2.11 (10.6.2.11) 56(84) bytes of data.
    64 bytes from 10.6.2.11: icmp_seq=1 ttl=63 time=5.36 ms
    64 bytes from 10.6.2.11: icmp_seq=2 ttl=63 time=6.21 ms
    64 bytes from 10.6.2.11: icmp_seq=3 ttl=63 time=5.40 ms
    64 bytes from 10.6.2.11: icmp_seq=4 ttl=63 time=4.19 ms

    --- 10.6.2.11 ping statistics ---
    4 packets transmitted, 4 received, 0% packet loss, time 3009ms
    rtt min/avg/max/mdev = 4.194/5.289/6.210/0.718 ms

<br />

## II. LAN clients

### 2. Client

<br />

**☀ Prouvez que...**

    tao@client1:~$ ip a
        inet 10.6.1.37/24 metric 100 brd 10.6.1.255 scope global dynamic enp0s8


    tao@client1:~$ resolvectl
    Link 2 (enp0s8)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS
                    DNSSEC=no/unsupported
    Current DNS Server: 1.1.1.1
        DNS Servers: 1.1.1.1


    tao@client1:~$ ip r s
    default via 10.6.1.254 dev enp0s8 proto dhcp src 10.6.1.37 metric 100
    1.1.1.1 via 10.6.1.254 dev enp0s8 proto dhcp src 10.6.1.37 metric 100
    10.6.1.0/24 dev enp0s8 proto kernel scope link src 10.6.1.37 metric 100
    10.6.1.254 dev enp0s8 proto dhcp scope link src 10.6.1.37 metric 100


    tao@client1:~$ ping www.ynov.com
    PING www.ynov.com (104.26.10.233) 56(84) bytes of data.
    64 bytes from 104.26.10.233: icmp_seq=1 ttl=52 time=31.0 ms
    64 bytes from 104.26.10.233: icmp_seq=2 ttl=52 time=26.5 ms
    64 bytes from 104.26.10.233: icmp_seq=3 ttl=52 time=28.2 ms
    64 bytes from 104.26.10.233: icmp_seq=4 ttl=52 time=33.4 ms
    
    --- www.ynov.com ping statistics ---
    4 packets transmitted, 4 received, 0% packet loss, time 3013ms
    rtt min/avg/max/mdev = 26.481/29.777/33.423/2.652 ms

<br />

## III. LAN serveurzzzz

### 1. Serveur Web

#### 3. Analyse et test

<br />

**☀ Déterminer sur quel port écoute le serveur NGINX**

    [root@web tao]# ss -lnpt | grep 80
    LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=11300,fd=6),("nginx",pid=11299,fd=6))
    LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=11300,fd=7),("nginx",pid=11299,fd=7))

<br />

**☀ Ouvrir ce port dans le firewall**

    [root@web tao]# firewall-cmd --permanent --add-port=80/tcp
    success

    [root@web tao]# firewall-cmd --reload
    success

<br />

**☀ Visitez le site web !**

    tao@client1:~$ curl http://10.6.2.11
    <!doctype html>
    <html>
    <head>
        <meta charset='utf-8'>
        <meta name='viewport' content='width=device-width, initial-scale=1'>
        <title>HTTP Server Test Page powered by: Rocky Linux</title>
        <style type="text/css">

<br />

### 2. Serveur DNS

#### 4. Analyse du service

<br />

**☀ Déterminer sur quel(s) port(s) écoute le service BIND9**

    [root@dns tao]# ss -lnmp | grep named
    udp   UNCONN 0      0                                       10.6.2.12:53               0.0.0.0:*    users:(("named",pid=764,fd=43))
    udp   UNCONN 0      0                                       10.6.2.12:53               0.0.0.0:*    users:(("named",pid=764,fd=6))
    udp   UNCONN 0      0                                       127.0.0.1:53               0.0.0.0:*    users:(("named",pid=764,fd=33))
    udp   UNCONN 0      0                                       127.0.0.1:53               0.0.0.0:*    users:(("named",pid=764,fd=32))
    udp   UNCONN 0      0                                           [::1]:53                  [::]:*    users:(("named",pid=764,fd=38))
    udp   UNCONN 0      0                                           [::1]:53                  [::]:*    users:(("named",pid=764,fd=39))
    tcp   LISTEN 0      10                                      10.6.2.12:53               0.0.0.0:*    users:(("named",pid=764,fd=45))
    tcp   LISTEN 0      10                                      10.6.2.12:53               0.0.0.0:*    users:(("named",pid=764,fd=44))
    tcp   LISTEN 0      4096                                    127.0.0.1:953              0.0.0.0:*    users:(("named",pid=764,fd=31))
    tcp   LISTEN 0      10                                      127.0.0.1:53               0.0.0.0:*    users:(("named",pid=764,fd=36))
    tcp   LISTEN 0      10                                      127.0.0.1:53               0.0.0.0:*    users:(("named",pid=764,fd=34))
    tcp   LISTEN 0      4096                                        [::1]:953                 [::]:*    users:(("named",pid=764,fd=42))
    tcp   LISTEN 0      10                                          [::1]:53                  [::]:*    users:(("named",pid=764,fd=40))
    tcp   LISTEN 0      10                                          [::1]:53                  [::]:*    users:(("named",pid=764,fd=41))

<br />

**☀️ Ouvrir ce(s) port(s) dans le firewall**

    [root@dns tao]# firewall-cmd --permanent --add-port=53/tcp
    success

    [root@dns tao]# firewall-cmd --permanent --add-port=953/tcp
    success

    [root@dns tao]# firewall-cmd --permanent --add-port=53/udp
    success

    [root@dns tao]# firewall-cmd --reload
    success


    [root@dns tao]# firewall-cmd --list-all
        ports: 22/tcp 22/udp 22/sctp 22/dccp 53/tcp 953/tcp 53/udp

<br />

#### 5. Tests manuels

<br />

**☀ Effectuez des requêtes DNS manuellement depuis le serveur DNS lui-même dans un premier temps**

    [root@dns tao]# dig web.tp6.b1 @10.6.2.12
    ; <<>> DiG 9.16.23-RH <<>> web.tp6.b1 @10.6.2.12
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 36211
    ;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

    [root@dns tao]# dig dns.tp6.b1 @10.6.2.12
    ; <<>> DiG 9.16.23-RH <<>> dns.tp6.b1 @10.6.2.12
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 15263
    ;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

    [root@dns tao]# dig ynov.com @10.6.2.12
    ; <<>> DiG 9.16.23-RH <<>> ynov.com @10.6.2.12
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 65520
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

    [root@dns tao]# dig -x 10.6.2.11 @10.6.2.12
    ; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.11 @10.6.2.12
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 3501
    ;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

    [root@dns tao]# dig -x 10.6.2.12 @10.6.2.12
    ; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.12 @10.6.2.12
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39796
    ;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

<br />

**☀ Effectuez une requête DNS manuellement depuis client1.tp6.b1**

    tao@client1:~$ dig web.tp6.b1
    ; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> web.tp6.b1
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 24586
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1
