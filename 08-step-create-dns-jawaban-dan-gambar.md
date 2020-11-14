Step Install Web server (NGINX)
1. pertama pastikan update sistem kita terlebih dahulu
    gunakan command sudo apt-update && apt-upgrade
2. sudo apt install nginx => untuk menginstall package nginx.
3. setelah ter install, verifikasi status nginx dengan cara mengetikkan command systemctl status nginx.
    Apakah sudah running atau belum, jika belum dapat dijalankan dengan command systemctl enable nginx / service enable nginx.
4. update firewall setting (sudo ufw allow )
5. test instalasi menggunakan browser & command line
    1. check menggunakan ip-addr/localhost di web-browser
        dapat dilihat pada gambar 
    2. menggunakan command line, curl -i http:/192.168.100.99(ip-address server)
6. check nginx status 
    check menggunakan command : "systemctl status nginx"

Step instalasi dns menggunakan bind9
Bind server iP (ubuntu) = 192.168.100.99
Domain name server = dumbways-hendrick.xyz
private network = 192.168.100.0/24
1. install package bind9 dan dependecnya.
    sudo apt-get install bind9 bind9utils bind9-doc dnsutils
2. check settingan  pada /etc/bind/named.conf.options isikan dengan field dibawah. 
        options {
        directory "/var/cache/bind";
        auth-nxdomain no;    # conform to RFC1035
     // listen-on-v6 { any; };
        listen-on port 53 { localhost; 192.168.0.0/24; };
        allow-query { localhost; 192.168.0.0/24; };
        forwarders { 8.8.8.8; };
        recursion yes;
        };
3. konfigurasi file pada /etc/bind/named.conf.local , isi dengan field dibawah ini:
    zone    "dumbways-hendrick.xyz" //nama domain yang akan kita gunakan 
     {
        type master;
        file    "/etc/bind/forward.dumbways-hendrick.local";
    };

    zone   "100.168.192.in-addr.arpa"   //ini merupakan reverse ip     
    {
       type master;
       file    "/etc/bind/reverse.dumbways-hendrick.local";
    };
    pastikan nama file di zone atas dan arpa harus sama namanya dengan konfigurasi difile diatas. save dan keluar dari terminal.
 
 4. buat file baru untuk forward lookup zone file, kita akan menduplikat file yg ada pada /etc/bind/db.local.
    jalan kan perintah 
        cp db.local forward-dumbways-hendrick.local
    kemudian ubah konfigurasi filenya seperti dibawah ini :
        $TTL    604800

        @       IN      SOA     primary.dumbways-hendrick.xyz. root.primary.dumbways-hendrick.xyz. (
                                    6         ; Serial
                                604820         ; Refresh
                                86600         ; Retry
                                2419600         ; Expire
                                604600 )       ; Negative Cache TTL

        ;Name Server Information
        @       IN      NS      primary.dumbways-hendrick.xyz.

        ;IP address of Your Domain Name Server(DNS)
        primary IN       A      192.168.100.99

        ;Mail Server MX (Mail exchanger) Record
        dumbways-hendrick.xyz. IN  MX  10  mail.dumbways-hendrick.xyz.

        ;A Record for Host names
        www     IN       A       192.168.100.99
        mail    IN       A       192.168.100.99

        ;CNAME Record
        ftp     IN      CNAME    www.dumbways-hendrick.xyz.

5.  buat file baru untuk reverse lookup zone file, kita akan menduplikat file yg ada pada /etc/bind/db.local.
    jalan kan perintah 
        cp db.127 forward-dumbways-hendrick.local
    kemudian ubah konfigurasi filenya seperti dibawah ini :
        ;
        ; BIND reverse data file for local loopback interface
        ;
        $TTL    604800
        @       IN      SOA     dumbways-hendrick.xyz. root.dumbways-hendrick.xyz. (
                                    21         ; Serial
                                604820         ; Refresh
                                864500        ; Retry
                                2419270         ; Expire
                                604880 )       ; Negative Cache TTL

        ;Your Name Server Info
        @       IN      NS      primary.dumbways-hendrick.xyz.
        primary IN      A       192.168.100.99

        ;Reverse Lookup for Your DNS Server
        99      IN      PTR     primary.dumbways-hendrick.xyz.

        ;PTR Record IP address to HostName
        99      IN      PTR     www.dumbways-hendrick.xyz.
        99      IN      PTR     mail.dumbways-hendrick.xyz.
save dan keluar dari editor, saatnya untuk memvalidasi file config bind9 pada zone files.

6.  a. untuk validasi zone file menggunakan command "sudo named-checkconf /etc/bind/named.conf.local" apabila tidak ada syntac error maka berhasil.selamat.
    b. jalankan service bin9 dan enable, serta check statusnya
    c. ubah dns server pada /etc/resolv.conf dan isikan sesuai dengan dns yang kita gunakan.
    d. testing dns menggunakan dig & nslookup.

FYI : Gambar pada folder images.
    untuk angka 01 -> menandakan soal untuk nomor 1
    untuk angka 08 -> menandakan soal untuk nomor 8
    begitu seterusnya.
Terimakasih.
Selesai---
