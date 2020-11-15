# Jarkom_Modul2_Praktikum_A05
- 05111840000030 MUHAMMMAD DAFFA’ AFLAH SYARIF
- 05111840000163 PUTU PUTRI NATIH DEVAYANTI

# Catatan Penting !!!
Disarankan untuk mengganti password user kelompok

Selalu mem-backup konfigurasi pada setiap UML untuk mengantisipasi kejadian yang tidak diinginkan. Backup disimpan diluar UML

yyy -> a05

IP PROBOLINGGO : NID_DMZ_tiap_kelompok+4 -> `10.151.73.52` (IP lainnya sama)

Install php5, jika tidak bisa install php7.0

File pendukung :

- Pendukung https://semeruyyy.pw didownload dengan cara `wget 10.151.36.202/semeru.pw.zip`
- Pendukung https://penanjakan.semeruyyy.pw didownload dengan cara `wget 10.151.36.202/penanjakan.semeru.pw.zip`
- Pendukung https://naik.gunung.semeruyyy.pw didownload dengan cara `wget 10.151.36.202/naik.gunung.semeru.pw.zip`

# SOAL
![praktikum3](https://user-images.githubusercontent.com/52326074/98698366-83f0b400-23a8-11eb-9daa-a1bf268600e6.jpg)

Sebelum mengerjakan soal, memasatikan untuk menjalankan perintah berikut :

- Ketikkan ` iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16` pada router SURABAYA agar client GRESIK dan SIDOARJO bisa terhubung ke internet
- Export proxy pada setiap UML
```
export http_proxy=”http://DPTSI-562908-c9986:40a5e@proxy.its.ac.id:8080”
export https_proxy=”http://DPTSI-562908-c9986:40a5e@proxy.its.ac.id:8080”
export ftp_proxy=”http://DPTSI-562908-c9986:40a5e@proxy.its.ac.id:8080”
```

## 1. Alamat https://semeruyyy.pw -> `https://semerua05.pw`
- Buka MALANG dan update package lists dengan menjalankan command `apt-get update`
- Install aplikasi bind9 pada MALANG `apt-get install bind9 -y`
- Pada MALANG lakukan perintah `nano /etc/bind/named.conf.local`
- Konfigurasi domain semerua05.pw berisi:
```
zone "semerua05.pw" {
	type master;
	file "/etc/bind/jarkom/semerua05.pw";
};
```
- Buat folder jarkom pada directory /etc/bind dengan command `mkdir /etc/bind/jarkom`
- Salin file db.local pada /etc/bind ke dalam folder jarkom dengan perintah `cp /etc/bind/db.local /etc/bind/jarkom/semerua05.pw`
-Buka dan edit file semerua05.pw dengan perintah `nano /etc/bind/jarkom/semerua05.pw` seperti pada gambar dibawah ini

![1a](https://user-images.githubusercontent.com/52326074/98806455-d1722d00-244b-11eb-9621-c02f013a4686.png)

- Kemudian restart bind9 dengan perintah `service bind9 restart`

![1b](https://user-images.githubusercontent.com/52326074/98806448-cf0fd300-244b-11eb-87f7-65281be58728.png)

- Pada client GRESIK dan SIDOARJO arahkan nameserver menuju IP MALANG dengan mengedit file resolve.conf dengan perintah `nano /etc/resolv.conf`
```
nameserver 10.151.73.50     #IP MALANG
```
- Untuk mencoba koneksi DNS, lakukan ping domain semerua05.pw dengan melakukan perintah berikut pada client GRESIK dan SIDOARJO `ping semerua05.pw`

![1c](https://user-images.githubusercontent.com/52326074/98806707-2dd54c80-244c-11eb-92ca-6e446e3d45d3.jpg)

## 2. Alias https://www.semeruyyy.pw -> ` https://www.semerua05.pw`
- Menambahkan konfigurasi pada server MALANG di dalam file semerua05.pw dengan command `nano /etc/bind/jarkom/semerua05.pw`
```
www	IN	CNAME	semerua05.pw.
```

![2a](https://user-images.githubusercontent.com/52326074/98806902-768d0580-244c-11eb-96b3-6df87da382a9.jpg)

- Kemudian restart bind9 dengan perintah `service bind9 restart`

![2b](https://user-images.githubusercontent.com/52326074/98806897-74c34200-244c-11eb-932d-765a4fff0f4d.jpg)

- Lalu cek di client GRESIK `www.semerua05.pw`

![2c](https://user-images.githubusercontent.com/52326074/98806900-75f46f00-244c-11eb-917d-71c42a3511c7.jpg)

## 3. Subdomain https://penanjakan.semeruyyy.pw -> `https://penanjakan.semerua05.pw`
- Edit file semerua05.pw pada MALANG dengan perintah `nano /etc/bind/jarkom/semerua05.pw` dengan menambahkan konfigurasi didalamnya
```
penanajakan	IN	A	10.151.73.52	; IP PROBOLINGGO
```

![3a](https://user-images.githubusercontent.com/52326074/98807682-9a048000-244d-11eb-9266-46c0f42c2f07.jpg)

- Edit `nano /etc/bind/named.conf.local`
```
zone "semerua05.pw" {
	type master;
	notify yes;
	also-notify { 10.151.73.52; }; //IP PROBOLINGGO
	also-transfer { 10.151.73.52; }; //IP PROBOLINGGO
	file "/etc/bind/jarkom/semerua05.pw";
};
```
- Kemudian restart bind9 dengan perintah `service bind9 restart`
- Lalu cek di client GRESIK `ping www.semerua05.pw`

![3b](https://user-images.githubusercontent.com/52326074/98807686-9bce4380-244d-11eb-948f-a22d17fbf876.jpg)

## 4. Reverse domain untuk domain utama
- Edit file nano /etc/bind/named.conf.local pada MALANG
```
zone "73.151.10.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/73.151.10.in-addr.arpa";
};
```
- Copykan file db.local ke dalam file 73.151.10.in-addr.arpa pada folder jarkom dengan perintah `cp /etc/bind/db.local /etc/bind/jarkom/73.151.10.in-addr.arpa`
- `73.151.10` merupakan 3 byte pertama IP MALANG yang di-reverse urutannya
- Kemudian edit file dengan `nano /etc/bind/jarkom/73.151.10.in-addr.arpa` dengan menambahkan konfigurasi  didalamnya
```
50 IN	PTR	semerua05.pw.	;IP MALANG
```
- Kemudian restart bind9 dengan perintah `service bind9 restart`
- Untuk mengecek konfigurasi dapat melakukan perintah `host -t PTR 10.151.73.50` pada client GRESIK

![4](https://user-images.githubusercontent.com/52326074/98808134-45add000-244e-11eb-8662-801a95b65821.jpg)

## 5. DNS Slave pada MOJOKETO
- Pada server MALANG edit file /etc/bind/named.conf.local dan sesuaikan dengan syntax:
```
zone "semerua05.pw" {
    type master;
    notify yes;
    also-notify { 10.151.73.51; }; // IP MOJOKERTO
    allow-transfer { 10.151.73.51; }; // MOJOKERTO
    file "/etc/bind/jarkom/semerub12.pw";
};
```
- Kemudian restart bind9 dengan perintah `service bind9 restart`

![5a](https://user-images.githubusercontent.com/52326074/98808484-c371db80-244e-11eb-9847-549dce310244.png)

- Pada MOJOKERTO update package lists dengan menjalankan command `apt-get update`
- Kemudian install aplikasi bind9 pada MOJOKERTO `apt-get install bind9 -y`
- Edit file pada MOJOKERTO `nano /etc/bind/named.conf.local` dengan konfigurasi:
```
zone "semerua05.pw" {
    type slave;
    masters { 10.151.73.50; }; //IP MALANG
    file "/var/lib/bind/semerua05.pw";
};
```
- Kemudian restart bind9 pada MOJOKERTO dengan perintah `service bind9 restart`

![5b](https://user-images.githubusercontent.com/52326074/98808476-c076eb00-244e-11eb-9400-f85c44339ea1.jpg)

- Pada sever MALANG matikan service bind9 dengan perintah `service bind9 stop`
- Pada client GRESIK atur nameserver mengarah ke IP MALANG dan MOJOKERTO `nano /etc/resolv.conf`

![5c](https://user-images.githubusercontent.com/52326074/98808477-c1a81800-244e-11eb-8a08-7b8c3b01df59.jpg)

- Lakukan `ping semerua05.pw` pada client GRESIK

![5d](https://user-images.githubusercontent.com/52326074/98808479-c240ae80-244e-11eb-9438-98b058368f6c.jpg)

## 6. Subdomain dengan alamat https://gunung.semeruyyy.pw -> `https://gunung.semerua05.pw` yang didelegasikan pada server MOJOKERTO dan mengarahkan ke IP PROBOLINGGO
MALANG

- Edit file `nano /etc/bind/jarkom/semerua05.pw`
- Tambahkan konfigurasi
```
ns1	IN	A	10.151.73.52	; IP PROBOLINGGO
naik	IN	NS	ns1
```

![6b](https://user-images.githubusercontent.com/52326074/98809026-93770800-244f-11eb-86a4-843468b2421d.jpg)

- Edit `nano /etc/bind/named.conf.options`
- Comment kan dnssec-validation auto; menjadi `//dnssec-validation auto;`
- Tambahkan `allow-query{any;};`
- Edit `nano /etc/bind/named.conf.local` dan tambahkan
```
zone "semerua05.pw" {
    type master;
    allow-transfer { 10.151.73.51; }; // MOJOKERTO
    file "/etc/bind/jarkom/semerua05.pw";
};
```
- Kemudian restart bind9 dengan perintah `service bind9 restart`

MOJOKERTO

- Edit `nano /etc/bind/named.conf.options`
- Comment kan `//dnssec-validation auto;`
- Tambahkan `allow-query{any;};`
- Edit file `nano /etc/bind/named.conf.local` dan tambahkan
```
zone "gunung.semerua05.pw" {
    type master;
    file "/etc/bind/delegasi/gunung.semerua05.pw";
    allow-transfer { any; };
};
```

![6a](https://user-images.githubusercontent.com/52326074/98809038-95d96200-244f-11eb-93cc-88f65ef1b313.jpg)

- Buat directory delegasi `mkdir /etc/bind/delegasi`
- Copykan db.local ke dalam gunung.semerua05.pw `cp /etc/bind/db.local /etc/bind/delegasi/gunung.semerub12.pw`
- Edit `nano /etc/bind/delegasi/gunung.semerua05.pw`
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     gunung.semerua05.pw. root.gunung.semerua05.pw. (
                        2020111001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      gunung.semerua05.pw.
@       IN      A       10.151.73.52 ;IP PROBOLINGGO
```
- Kemudian restart bind9 dengan perintah `service bind9 restart`
- Lakukan testing pada GRESIK `ping gunung.semerua05.pw`

![6c7b](https://user-images.githubusercontent.com/52326074/98809033-94a83500-244f-11eb-8346-f7c8fdf0b6c7.jpg)

## 7. Subdomain dengan alamat https://naik.gunung.semeruyyy.pw -> `https://naik.gunung.semerua05.pw` domain ini diarahkan ke IP PROBOLINGGO
- Pada MOJOKERTO edit `nano /etc/bind/delegasi/gunung.semerub12.pw` dan tambahkan
```
naik       IN      A       10.151.73.52 ;IP PROBOLINGGO
```
- Kemudian restart bind9 dengan perintah `service bind9 restart`

![7a](https://user-images.githubusercontent.com/52326074/98809174-b86b7b00-244f-11eb-80c8-b12ec168c8b5.jpg)

- Lakukan testing pada GRESIK `ping naik.gunung.semerua05.pw`

![6c7b](https://user-images.githubusercontent.com/52326074/98809033-94a83500-244f-11eb-8346-f7c8fdf0b6c7.jpg)

## 8. Domain https://semeruyyy.pw -> `https://semerua05.pw` memiliki DocumentRoot pada /var/www/semeruyyy.pw -> `/var/www/semerua05.pw`. Awalnya dapat diakses menggunakan alamat https://semeruyyy.pw/index.php/home
- Jalankan perintah `apt-get install apache2`
- Jalankan perintah `apt-get install php5`
- Pindah ke directory /etc/apache2/sites-available dengan perintah cd /etc/apache2/sites-available
- Copy file default menjadi file `semerua05.pw` dengan perintah `cp default semerua05.pw`.
- Buka file `semerua05.pw` lalu tambahkan
 ```
 ServerName semerua05.pw
 ServerAlias www.semerua05.pw
```
- Ubah DocumentRoot menjadi `/var/www/semerua05.pw`
- Aktifkan konfigurasi semerua05.pw dengan menggunakan perintah `a2ensite semerua05.pw`
- Restart apache dengan perintah `service apache2 restart`
- Pindah ke directory  `/var/www` dan lakukan download file dengan `wget 10.151.36.202/semeru.pw.zip` 
- Unzip file dengan perintah `unzip semeru.pw.zip` dan kemudian rename menjadi `semerua05.pw`
- Buka browser dan akses `semerua05.pw`. Akan muncul tampilan sebagai berikut. 

![8](https://user-images.githubusercontent.com/52326074/98809961-016fff00-2451-11eb-8570-307325054d36.jpg)

## 9. Awalnya dapat diakses menggunakan alamat https://semeruyyy.pw/index.php/home -> `https://semerua05.pw/index.php/home` kemudian url di mod rewrite menjadi https://semeruyyy.pw/home -> `https://semerua05.pw/home`
- Aktifkan module rewrite dengan menjalankan perintah `a2enmod rewrite`
- Restart apache dengan perintah `service apache2 restart`
- Pindah ke directory `/var/www/semerua05.pw` dan buat file `.htaccess` dengan isi file
```
 RewriteEngine On
 RewriteCond %{REQUEST_FILENAME} !-d
 RewriteRule ^([^\.]+)$ /index.php/$1 [NC,L]
```
 
![9~](https://user-images.githubusercontent.com/52326074/98810601-0e412280-2452-11eb-8aa0-d457c0a4fb1a.png)

- Pindah ke directory /etc/apache2/sites-available kemudian buka file semerua05.pw dan tambahkan
```
<Directory /var/www/semerua05.pw>
     Options +FollowSymLinks -Multiviews
     AllowOverride All
 </Directory>
 ```
 - Restart apache dengan perintah `service apache2 restart`
 - Buka browser dan akses `https://semerua05.pw/home`

![9](https://user-images.githubusercontent.com/52326074/98809955-ffa63b80-2450-11eb-8188-14a25657dc0c.jpg)

## 10. Web https://penanjakan.semeruyyy.pw -> `https://penanjakan.semerua05.pw` digunakan untuk menyimpan assets file yang memiliki DocumentRoot pada /var/www/penanjakan.semeruyyy.pw -> `/var/www/penanjakan.semerua05.pw` dan memiliki folder sebagai berikut.
```
/var/www/penanjakan.semeruyyy.pw
                                /public/javascripts
                                /public/css
                                /public/images
                                /errors
```
- Pindah ke directory `/etc/apache2/sites-available` dengan perintah `cd /etc/apache2/sites-available`
- Copy file default menjadi file `penanjakan.semerua05.pw`
- Buka file penanjakan.semerub12.pw, lalu tambahkan
```
 ServerName penanjakan.semerua05.pw
 ServerAlias www.penanjakan.semerua05.pw
```
- Kemudian ubah DocumentRoot menjadi `/var/www/penanjakan.semerua05.pw`

![1011a](https://user-images.githubusercontent.com/52326074/98816038-a93dfa80-245a-11eb-83eb-d2f1d93cbbec.png)

- Gunakan perintah `a2ensite penanjakan.semerua05.pw` untuk mengaktifkan konfigurasi semerua05.pw
- Gunakan perintah `service apache2 restart` untuk merestart apache
- Pindah ke directory `/var/www` dan gunakan perintah `wget 10.151.36.202/penanjakan.semeru.pw.zip` untuk mendownload file
- Unzip file kemudian rename dengan menggunakan perintah `mv penanjakan.semeru.pw penanjakan.semerua05.pw`
- Buka browser dan akses `https://penanjakan.semerua05.pw`

![1011d](https://user-images.githubusercontent.com/52326074/98816031-a6430a00-245a-11eb-9106-0299b9033efe.jpg)

- Kemudian buka folder `public`

![1011e](https://user-images.githubusercontent.com/52326074/98816033-a6dba080-245a-11eb-8402-e374aa126b60.jpg)

- Jika mengakses `errors`

![10f](https://user-images.githubusercontent.com/52326074/98816035-a80ccd80-245a-11eb-8008-68595b0783c6.jpg)


## 11. Pada folder `/public` dibolehkan directory listing namun untuk folder didalamnya tidak boleh
- Pindah ke directory etc/apache2/sites-available
- Buka file `penanjakan.semerua05.pw`, tambahkan konfigurasi berikut. 

![1011a](https://user-images.githubusercontent.com/52326074/98816038-a93dfa80-245a-11eb-83eb-d2f1d93cbbec.png)

![1011b](https://user-images.githubusercontent.com/52326074/98816039-a9d69100-245a-11eb-9eb2-cea26b355067.png)

![1011c](https://user-images.githubusercontent.com/52326074/98816025-a4794680-245a-11eb-99fb-f5a3d4b542d9.png)

- Gunakan perintah `service apache2 restart` untuk merestart apache
- Akses `penanjakan.semerua05.pw` dan buka folder `public`

![1011d](https://user-images.githubusercontent.com/52326074/98816031-a6430a00-245a-11eb-9106-0299b9033efe.jpg)

- Buka masing-masing foldernya. Lalu akan muncul gambar berikut. 

![1011e](https://user-images.githubusercontent.com/52326074/98816033-a6dba080-245a-11eb-8402-e374aa126b60.jpg)


## 12. Mengatasi HTTP Error code 404 disediakan file `404.html` pada folder `/errors`
- Pindah ke directory etc/apache2/sites-available
- Kemudian buka `penanjakan.semerua05.pw`
- Tambahkan `ErrorDocument 404 /errors/404.html`

![12a](https://user-images.githubusercontent.com/52326074/98816275-fe7a0c00-245a-11eb-8aac-daa2b7ed8bc7.jpg)

- Gunakan perintah service apache2 restart untuk merestart apache

![12b](https://user-images.githubusercontent.com/52326074/98816266-fc17b200-245a-11eb-9b7f-1e783f6fdf17.png)

- Hasilnya adalah sebagai berikut. 

![12c](https://user-images.githubusercontent.com/52326074/98816271-fd48df00-245a-11eb-9d0c-83bf81d2662a.jpg)

## 13. Untuk mengakses file assets javascript yang awalnya menggunakan url https://penanjakan.semeruyyy.pw/public/javascripts -> `https://penanjakan.semerua05.pw/public/javascripts` kemudian url di mod rewrite menjadi https://penanjakan.semeruyyy.pw/js -> `https://penanjakan.semerua05.pw/js`
- Pindah ke directory etc/apache2/sites-available
- Kemudian buka file `penanjakan.semerua05.pw`
- Tambahkan Alias  `"/js" "/var/www/penanjakan.semerua05.pw/public/javascripts"`

![13a](https://user-images.githubusercontent.com/52326074/98818691-7bf34b80-245e-11eb-9a9d-c777b0ad5b70.jpg)

- Hasil : 

![13b](https://user-images.githubusercontent.com/52326074/98818697-7dbd0f00-245e-11eb-927a-1deca7698a83.png)

## 14. Web https://naik.gunung.semeruyyy.pw -> `https://naik.gunung.semerua05.pw` sudah bisa diakses hanya dengan port 8888
- Buka file `ports.conf` di `/etc/apache2`
- Tambahkan `port 8888`
- Pindah ke directory `/etc/apache2/sites-available` dengan perintah `cd /etc/apache2/sites-available`
- Copy file default menjadi file `naik.gunung.semerua05.pw`
- Buka file `naik.gunung.semerua05.pw` 
- Setting virtual host di port 8888: `<VirtualHost *:8888>`

![14b](https://user-images.githubusercontent.com/52326074/98818677-7990f180-245e-11eb-8a8c-220455852aa7.png)

- Lalu tambahkan 
```
 ServerName naik.gunung.semerua05.pw
 ServerAlias www.naik.gunung.semerua05.pw
 ```
- Kemudian ubah DocumentRoot menjadi `/var/www/naik.gunung.semerua05.pw`
- Gunakan perintah `a2ensite naik.gunung.semerua05.pw` untuk mengaktifkan konfigurasi `semerua05.pw`
- Pindah ke directory `/var/www`
- Gunakan perintah `wget 10.151.36.202/naik.gunung.semeru.pw.zip` untuk mendownload file
- Unzip file kemudian direname menjadi `naik.gunung.semerua05.pw`
- Akses `naik.gunung.semerua05.pw:8888` 

![14c](https://user-images.githubusercontent.com/52326074/98824136-8238f600-2465-11eb-9364-92c0c44bb47e.jpg)

## 15. Karena https://naik.gunung.semeruyyy.pw -> `https://naik.gunung.semerua05.pw` private, selanjutnya membuat autentifikasi dengan username `semeru` dan password `kuynaikgunung` agar aman dan tidak sembarang orang mengaksesnya
- Install apache utilites package dengan 
```
apt-get update
apt-get install apache2 apache2-utils
```
- Kemudian masukkan perintah `htpasswd -c /etc/apache2/.htpasswd semeru`
- Masukkan password `kuynaikgunung`
- Edit file `etc/apache2/sites-enabled/naik.gunung.semerua05.pw` untuk menambahkan Auth, seperti:
```
<Directory /var/www/naik.semerua05.pw>
     AuthType Basic
     AuthName "Restricted Content"
     AuthUserFile /etc/apache2/.htpasswd
     Require valid-user
 </Directory>
 ```
 
 ![15a](https://user-images.githubusercontent.com/52326074/98824133-81a05f80-2465-11eb-9e4b-808ef3bb5c52.jpg)
 
 - Gunakan perintah `service apache2 restart` untuk merestart apache
 - Buka browser dan akses `naik.gunung.semerua05.pw:8888`
 - Masukkan username `semeru` dan password `kuynaikgunung`

![15b](https://user-images.githubusercontent.com/52326074/98824121-7e0cd880-2465-11eb-9126-ac5251c26617.jpg)

## 16. IP PROBOLINGGO dialihkan secara otomatis ke https://semeruyyy.pw -> `https://semerua05.pw`
- Buka browser dan akses `10.151.73.52` yang merupakan IP probolinggo untuk pengecekan awal.
- Mengedit file 000-default di `/var/www`

![16a](https://user-images.githubusercontent.com/52326074/98824123-7f3e0580-2465-11eb-9f8e-25398d2ff4db.jpg)

- Di direktori /var/www/ buat file .htaccess dengan isi
```
RewriteEngine On
RewriteBase /
RewriteCond %{HTTP_HOST} ^10\.151\.73\.52$
RewriteRule ^(.*)$ http://semerua05.pw/&1 [L,R=301]
```
- Gunakan perintah `service apache2 restart` untuk merestart apache
- Buka browser dan akses `10.151.73.52` yang merupakan IP PROBOLINGGO. Hasilnya akan sebagai berikut. 

![16b](https://user-images.githubusercontent.com/52326074/98824125-806f3280-2465-11eb-883f-b9dff3ec6ab5.jpg)

## 17. Karena pengunjung pada /var/www/penanjakan.semeruyyy.pw/public/images -> `/var/www/penanjakan.semerua05.pw/public/images` sangat banyak maka request gambar yang memiliki substring `semeru` akan diarahkan menuju semeru.jpg

- Pindah ke directory /var/www/penanjakan.semerua05.pw
- Buat file .htaccess dan diubah menjadi seperti gambar dibawah ini.

![17a](https://user-images.githubusercontent.com/52326074/98826269-10ae7700-2468-11eb-99aa-63318e8d6393.jpg)

- Gunakan perintah `service apache2 restart` untuk merestart apache

![17b](https://user-images.githubusercontent.com/52326074/98826265-0f7d4a00-2468-11eb-9fb3-e863e80a8124.jpg)

# TERIMA KASIH
