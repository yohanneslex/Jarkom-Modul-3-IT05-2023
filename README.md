# JARKOM-MODUL-3-IT05-2023
Yohannes Hasahatan Tua Alexandro - 5027211022

Arkan Hendri Abdul Ghani Burhan - 5027211026

## TOPOLOGI
![image](https://github.com/yohanneslex/Jarkom-Modul-3-IT05-2023/assets/50076171/8be92c37-c0d7-496c-abcd-40e335bd130b)

## CONFIG
Aura (DHCP Relay)
```sh
auto eth0
iface eth0 inet dhcp
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.66.0.0/16

auto eth1
iface eth1 inet static
	address 10.66.1.0
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.66.2.0
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.66.3.0
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 10.66.4.0
	netmask 255.255.255.0

```

Himmel (DHCP Server)
```sh
auto eth0
iface eth0 inet static
	address 10.66.1.1
	netmask 255.255.255.0
	gateway 10.66.1.0

```

Heiter (DNS Server)
```sh
auto eth0
iface eth0 inet static
	address 10.66.1.2
	netmask 255.255.255.0
	gateway 10.66.1.0
```

Denken (Database Server)
```sh
auto eth0
iface eth0 inet static
	address 10.66.2.1
	netmask 255.255.255.0
	gateway 10.66.2.0
```

Eisen (Load Balancer)
```sh
auto eth0
iface eth0 inet static
	address 10.66.2.2
	netmask 255.255.255.0
	gateway 10.66.2.0
```

Frieren (Laravel Worker)
```sh
auto eth0
iface eth0 inet static
	address 10.66.4.3
	netmask 255.255.255.0
	gateway 10.66.4.0

hwaddress ether 9e:d5:2c:df:39:32
```

Flamme (Laravel Worker)
```sh
auto eth0
iface eth0 inet static
	address 10.66.4.2
	netmask 255.255.255.0
	gateway 10.66.4.0

hwaddress ether da:cc:d9:29:59:e8
```

Fern (Laravel Worker)
```sh
auto eth0
iface eth0 inet static
	address 10.66.4.1
	netmask 255.255.255.0
	gateway 10.66.4.0

hwaddress ether 8a:31:c6:e6:a2:7b
```

Lawine (PHP Worker)
```sh
auto eth0
iface eth0 inet static
	address 10.66.3.3
	netmask 255.255.255.0
	gateway 10.66.3.0

hwaddress ether 8e:c1:16:c2:6d:4b
```

Linie (PHP Worker)
```sh
auto eth0
iface eth0 inet static
	address 10.66.3.2
	netmask 255.255.255.0
	gateway 10.66.3.0

hwaddress ether 7a:e7:1c:d2:ae:44
```

Lugner (PHP Worker)
```sh
auto eth0
iface eth0 inet static
	address 10.66.3.1
	netmask 255.255.255.0
	gateway 10.66.3.0

hwaddress ether 8a:02:fd:bb:05:be
```

Revolte, Richter, Sein, dan Stark (Client)
```sh
auto eth0
iface eth0 inet dhcp
```



## Soal 1

Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.

Kemudian, karena masih banyak spell yang harus dikumpulkan, bantulah para petualang untuk memenuhi kriteria berikut.:
Semua CLIENT harus menggunakan konfigurasi dari DHCP Server.

## Jawaban 
Lugner (PHP Worker)
```sh
auto eth0
iface eth0 inet static
	address 10.66.3.1
	netmask 255.255.255.0
	gateway 10.66.3.0
```

Fern (Laravel Worker)
```sh
auto eth0
iface eth0 inet static
	address 10.66.4.1
	netmask 255.255.255.0
	gateway 10.66.4.0
```

Script pada Node Heiter selaku DNS Server
```sh
echo 'zone "riegel.canyon.it05.com" {
    type master;
    file "/etc/bind/sites/riegel.canyon.it05.com";
};

zone "granz.channel.it05.com" {
    type master;
    file "/etc/bind/sites/granz.channel.it05.com";
};

zone "1.66.10.in-addr.arpa" {
    type master;
    file "/etc/bind/sites/1.66.10.in-addr.arpa";
};' > /etc/bind/named.conf.local

mkdir -p /etc/bind/sites
cp /etc/bind/db.local /etc/bind/sites/riegel.canyon.it05.com
cp /etc/bind/db.local /etc/bind/sites/granz.channel.it05.com
cp /etc/bind/db.local /etc/bind/sites/1.66.10.in-addr.arpa

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.it05.com. root.riegel.canyon.it05.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.it05.com.
@       IN      A       10.66.4.1     ; IP Fern
www     IN      CNAME   riegel.canyon.it05.com.' > /etc/bind/sites/riegel.canyon.it05.com

echo '
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.it05.com. root.granz.channel.it05.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.it05.com.
@       IN      A       10.66.3.1     ; IP Lugner
www     IN      CNAME   granz.channel.it05.com.' > /etc/bind/sites/granz.channel.it05.com

echo 'options {
      directory "/var/cache/bind";

      forwarders {
              192.168.122.1;
      };

      // dnssec-validation auto;
      allow-query{any;};
      auth-nxdomain no;    # conform to RFC1035
      listen-on-v6 { any; };
}; ' >/etc/bind/named.conf.options

service bind9 start
```


## Soal 2

Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80

## Jawaban 
Script setup pada Node Himmel selaku DHCP Server
```sh
echo 'subnet 10.66.1.0 netmask 255.255.255.0 {
}

subnet 10.66.2.0 netmask 255.255.255.0 {
}

subnet 10.66.3.0 netmask 255.255.255.0 {
    range 10.66.3.16 10.66.3.32;
    range 10.66.3.64 10.66.3.80;
    option routers 10.66.3.0;
}' > /etc/dhcp/dhcpd.conf
```


## Soal 3

Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168 

## Jawaban 
Script config pada switch4
```sh
echo 'subnet 10.66.1.0 netmask 255.255.255.0 {
}

subnet 10.66.2.0 netmask 255.255.255.0 {
}

subnet 10.66.3.0 netmask 255.255.255.0 {
    range 10.66.3.16 10.66.3.32;
    range 10.66.3.64 10.66.3.80;
    option routers 10.66.3.0;
}

subnet 10.66.4.0 netmask 255.255.255.0 {
    range 10.66.4.12 10.66.4.20;
    range 10.66.4.160 10.66.4.168;
    option routers 10.66.4.0;
} ' > /etc/dhcp/dhcpd.conf
```


## Soal 4

Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut

## Jawaban 
Script pada Node Heiter
```sh
subnet 10.66.3.0 netmask 255.255.255.0 {
    ...
    option broadcast-address 10.66.3.255;
    option domain-name-servers 10.66.1.2;
    ...
}

subnet 10.66.4.0 netmask 255.255.255.0 {
    option broadcast-address 10.66.4.255;
    option domain-name-servers 10.66.1.2;
} 
```
Shell script untuk dijalankan pada Node Heiter

```sh
echo 'subnet 10.66.1.0 netmask 255.255.255.0 {
}

subnet 10.66.2.0 netmask 255.255.255.0 {
}

subnet 10.66.3.0 netmask 255.255.255.0 {
    range 10.66.3.16 10.66.3.32;
    range 10.66.3.64 10.66.3.80;
    option routers 10.66.3.0;
    option broadcast-address 10.66.3.255;
    option domain-name-servers 10.66.1.2;
}

subnet 10.66.4.0 netmask 255.255.255.0 {
    range 10.66.4.12 10.66.4.20;
    range 10.66.4.160 10.66.4.168;
    option routers 10.66.4.0;
    option broadcast-address 10.66.4.255;
    option domain-name-servers 10.66.1.2;
} ' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server start
```

Script setup DHCP Relay
```sh
echo '# Defaults for isc-dhcp-relay initscript
# sourced by /etc/init.d/isc-dhcp-relay
# installed at /etc/default/isc-dhcp-relay by the maintainer scripts

#
# This is a POSIX shell fragment
#

# What servers should the DHCP relay forward requests to?
SERVERS="10.66.1.1"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth1 eth2 eth3 eth4"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""' > /etc/default/isc-dhcp-relay

service isc-dhcp-relay start 
```


## Soal 5

Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit

## Jawaban 
Script command pada DHCP Server
```sh
echo 'subnet 10.66.1.0 netmask 255.255.255.0 {
}

subnet 10.66.2.0 netmask 255.255.255.0 {
}

subnet 10.66.3.0 netmask 255.255.255.0 {
    range 10.66.3.16 10.66.3.32;
    range 10.66.3.64 10.66.3.80;
    option routers 10.66.3.0;
    option broadcast-address 10.66.3.255;
    option domain-name-servers 10.66.1.2;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 10.66.4.0 netmask 255.255.255.0 {
    range 10.66.4.12 10.66.4.20;
    range 10.66.4.160 10.66.4.168;
    option routers 10.66.4.0;
    option broadcast-address 10.66.4.255;
    option domain-name-servers 10.66.1.2;
    default-lease-time 720;
    max-lease-time 5760;
}

service isc-dhcp-server restart
```

#### Berjalannya waktu, petualang diminta untuk melakukan deployment.

## Soal 6

Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.

## Jawaban 
Setup pada seluruh Node PHP Worker
```sh
wget -O '/var/www/granz.channel.it05.com' 'https://drive.google.com/u/0/uc?id=1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1&export=download'
unzip -o /var/www/granz.channel.it05.com -d /var/www/
rm /var/www/granz.channel.it05.com
mv /var/www/modul-3 /var/www/granz.channel.it05.com
```

Konfigurasi NGINX pada PHP Worker
```sh
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/granz.channel.it05.com
ln -s /etc/nginx/sites-available/granz.channel.it05.com /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

echo 'server {
    listen 80;
    server_name _;

    root /var/www/granz.channel.it05.com;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.3-fpm.sock;  # Sesuaikan versi PHP dan socket
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}' > /etc/nginx/sites-available/granz.channel.it05.com

service nginx restart
```


## Soal 7

Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
- Lawine, 4GB, 2vCPU, dan 80 GB SSD.
- Linie, 2GB, 2vCPU, dan 50 GB SSD.
- Lugner 1GB, 1vCPU, dan 25 GB SSD.

aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.


## Jawaban 
Node DNS Server
```sh
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.it05.com. root.riegel.canyon.it05.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.it05.com.
@       IN      A       10.66.2.2     ; IP LB Eiken
www     IN      CNAME   riegel.canyon.it05.com.' > /etc/bind/sites/riegel.canyon.it05.com

echo '
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.it05.com. root.granz.channel.it05.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.it05.com.
@       IN      A       10.66.2.2     ; IP LB Eiken
www     IN      CNAME   granz.channel.it05.com.' > /etc/bind/sites/granz.channel.it05.com
```

Node Eisen
```sh
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/lb_php

echo ' upstream worker {
    server 10.66.3.1;
    server 10.66.3.2;
    server 10.66.3.3;
}

server {
    listen 80;
    server_name granz.channel.it05.com www.granz.channel.it05.com;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {
        proxy_pass http://worker;
    }
} ' > /etc/nginx/sites-available/lb_php

ln -s /etc/nginx/sites-available/lb_php /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

service nginx restart
```

Jalankan command pada Node Client Revolte
```sh
ab -n 1000 -c 100 http://www.granz.channel.it05.com/
```


## Soal 8

Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
- Nama Algoritma Load Balancer
- Report hasil testing pada Apache Benchmark
- Grafik request per second untuk masing masing algoritma. 
- Analisis 


## Jawaban 
Jalankan command pada Node Client Revolte
```sh
ab -n 200 -c 10 http://www.granz.channel.it05.com/ 
```


## Soal 9

Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.

## Jawaban 
Jalankan command pada Node Client Revolte
```sh
ab -n 200 -c 10 http://www.granz.channel.it05.com/
```


## Soal 10

Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/.

## Jawaban 
Script setup terlebih dahulu
```sh
mkdir /etc/nginx/rahasisakita
htpasswd -c /etc/nginx/rahasisakita/htpasswd netics
```
Lalu masukkan password yakni ```ajkit05```

Maka akan menghasilkan output sebagai berikut
```sh
auth_basic "Restricted Content";
auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;
```


## Soal 11

Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id.

## Jawaban 
Setup Script
```sh
location ~ /its {
    proxy_pass https://www.its.ac.id;
    proxy_set_header Host www.its.ac.id;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```

Script secara keseluruhan
```sh
echo 'upstream worker {
    server 10.66.3.1;
    server 10.66.3.2;
    server 10.66.3.3;
}

server {
    listen 80;
    server_name granz.channel.it05.com www.granz.channel.it05.com;

    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;

    location / {
        proxy_pass http://worker;
    }

    location ~ /its {
        proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}' > /etc/nginx/sites-available/lb_php
```

Command line yang akan dijalankan
```sh
lynx www.granz.channel.it05.com/its
```


## Soal 12

Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168.

## Jawaban 
Script setup
```sh
location / {
    allow 10.66.173.3.69;
    allow 10.66.173.3.70;
    allow 10.66.173.4.167;
    allow 10.66.173.4.168;
    deny all;
    proxy_pass http://worker;
}
```

Script secara kesuluruhan
```sh
echo 'upstream worker {
    server 10.66.3.1;
    server 10.66.3.2;
    server 10.66.3.3;
}

server {
    listen 80;
    server_name granz.channel.it05.com www.granz.channel.it05.com;

    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;

    location / {
        allow 10.66.3.69;
        allow 10.66.3.70;
        allow 10.66.4.167;
        allow 10.66.4.168;
        deny all;
        proxy_pass http://worker;
    }

    location /its {
        proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}' > /etc/nginx/sites-available/lb_php
```

#### Karena para petualang kehabisan uang, mereka kembali bekerja untuk mengatur riegel.canyon.yyy.com.

## Soal 13

Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern.

## Jawaban 
Setup pada Node Denken
```sh
echo '# This group is read both by the client and the server
# use it for options that affect everything
[client-server]

# Import all .cnf files from configuration directory
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mariadb.conf.d/

# Options affecting the MySQL server (mysqld)
[mysqld]
skip-networking=0
skip-bind-address
' > /etc/mysql/my.cnf
```

Mengubah bind address
```sh
cd /etc/mysql/mariadb.conf.d/50-server.cnf

# Changes
bind-address            = 0.0.0.0
```

Command line untuk dijalankan
```sh
mysql -u root -p
Enter password: 

CREATE USER 'kelompokait05'@'%' IDENTIFIED BY 'passwordait05';
CREATE USER 'kelompokait05'@'localhost' IDENTIFIED BY 'passwordait05';
CREATE DATABASE dbkelompokait05;
GRANT ALL PRIVILEGES ON *.* TO 'kelompokait05'@'%';
GRANT ALL PRIVILEGES ON *.* TO 'kelompokait05'@'localhost';
FLUSH PRIVILEGES;
```


## Soal 14

Frieren, Flamme, dan Fern memiliki Riegel Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer

## Jawaban 
Setup script install composer
```sh
wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
mv composer.phar /usr/local/bin/composer```

Setup script install git dan melakukan cloning
```sh
apt-get install git -y
cd /var/www && git clone https://github.com/martuafernando/laravel-praktikum-jarkom
cd /var/www/laravel-praktikum-jarkom && composer update
```

Konfigurasi seluruh node Worker
```sh
cd /var/www/laravel-praktikum-jarkom && cp .env.example .env
echo 'APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=10.66.2.1
DB_PORT=3306
DB_DATABASE=dbkelompokit05
DB_USERNAME=kelompokit05
DB_PASSWORD=passwordit05

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=10.0.0.1

REDIS_HOST=10.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"' > /var/www/laravel-praktikum-jarkom/.env
cd /var/www/laravel-praktikum-jarkom && php artisan key:generate
cd /var/www/laravel-praktikum-jarkom && php artisan config:cache
cd /var/www/laravel-praktikum-jarkom && php artisan migrate
cd /var/www/laravel-praktikum-jarkom && php artisan db:seed
cd /var/www/laravel-praktikum-jarkom && php artisan storage:link
cd /var/www/laravel-praktikum-jarkom && php artisan jwt:secret
cd /var/www/laravel-praktikum-jarkom && php artisan config:clear
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
```

Konfigurasi NGINX pada node Worker
```sh
echo 'server {
    listen <X>;

    root /var/www/laravel-praktikum-jarkom/public;

    index index.php index.html index.htm;
    server_name _;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
      include snippets/fastcgi-php.conf;
      fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

    location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/implementasi_error.log;
    access_log /var/log/nginx/implementasi_access.log;
}' > /etc/nginx/sites-available/laravel-worker
```


## Soal 15

Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire. POST /auth/register

## Jawaban
Script setup
```sh
echo '
{
  "username": "kelompokit05",
  "password": "passwordit05"
}' > register.json
```

Comman line untuk dijalankan
```sh
ab -n 100 -c 10 -p register.json -T application/json http://10.66.4.1:8001/api/auth/register
```


## Soal 16

Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire. POST /auth/login

## Jawaban 
echo '
{
  "username": "kelompokit09",
  "password": "passwordit09"
}' > login.json
```

Comman line untuk dijalankan
```sh
ab -n 100 -c 10 -p login.json -T application/json http://10.66.4.1:8001/api/auth/login
```


## Soal 17

Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire. GET /me


## Jawaban 
Script setup untuk endpoint
```sh
curl -X POST -H "Content-Type: application/json" -d @login.json http://10.66.4.1:8001/api/auth/login > login_output.txt
```

Comman line untuk  melakukan set token secara global
```sh
token=$(cat login_output.txt | jq -r '.token')
```

Comman line untuk melakukan testing
```sh
ab -n 100 -c 10 -H "Authorization: Bearer $token" http://10.66.4.1:8001/api/me
```


## Soal 18

Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari Frieren, Flamme, dan Fern.

## Jawaban
Script setup
```sh
echo 'upstream worker {
    server 10.66.4.1:8001;
    server 10.66.4.2:8002;
    server 10.66.4.3:8003;
}

server {
    listen 80;
    server_name riegel.canyon.it05.com www.riegel.canyon.it05.com;

    location / {
        proxy_pass http://worker;
    }
} 
' > /etc/nginx/sites-available/laravel-worker

ln -s /etc/nginx/sites-available/laravel-worker /etc/nginx/sites-enabled/laravel-worker

service nginx restart
```

Command line untuk menjalankan
```sh
ab -n 100 -c 10 -p login.json -T application/json http://www.riegel.canyon.it05.com/api/auth/login
```


## Soal 19

Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Frieren, Flamme, dan Fern. Untuk testing kinerja naikkan 
- pm.max_children
- pm.start_servers
- pm.min_spare_servers
- pm.max_spare_servers

sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada Grimoire.


## Jawaban 
Script 1
```sh
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 5
pm.start_servers = 2
pm.min_spare_servers = 1
pm.max_spare_servers = 3' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```

Script 2
```sh
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 25
pm.start_servers = 5
pm.min_spare_servers = 3
pm.max_spare_servers = 10' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```

Script 3
```sh
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 50
pm.start_servers = 8
pm.min_spare_servers = 5
pm.max_spare_servers = 15' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart```

Script 4
```sh
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 75
pm.start_servers = 10
pm.min_spare_servers = 5
pm.max_spare_servers = 20' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```


## Soal 20

Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second.

## Jawaban
Script
```sh
echo 'upstream worker {
    least_conn;
    server 10.66.4.1:8001;
    server 10.66.4.2:8002;
    server 10.66.4.3:8003;
}

server {
    listen 80;
    server_name riegel.canyon.it05.com www.riegel.canyon.it05.com;

    location / {
        proxy_pass http://worker;
    }
} 
' > /etc/nginx/sites-available/laravel-worker

service nginx restart
```
