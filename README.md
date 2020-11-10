# Jarkom_Modul2_Praktikum_A05
- MUHAMMMAD DAFFA’ AFLAH SYARIF    05111840000030
- PUTU PUTRI NATIH DEVAYANTI       05111840000163

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

1. Alamat https://semeruyyy.pw -> `https://semerua05.pw`

2. Alias https://www.semeruyyy.pw -> ` https://www.semerua05.pw`

3. Subdomain https://penanjakan.semeruyyy.pw -> `https://penanjakan.semerua05.pw`

4. Reverse domain untuk domain utama

5. DNS Slave pada MOJOKETO

6. Subdomain dengan alamat https://gunung.semeruyyy.pw -> `https://gunung.semerua05.pw` yang didelegasikan pada server MOJOKERTO dan mengarahkan ke IP PROBOLINGGO

7. Subdomain dengan alamat https://naik.gunung.semeruyyy.pw -> `https://naik.gunung.semerua05.pw` domain ini diarahkan ke IP PROBOLINGGO

8. Domain https://semeruyyy.pw -> `https://semerua05.pw` memiliki DocumentRoot pada /var/www/semeruyyy.pw -> `/var/www/semerua05.pw`

9. Awalnya dapat diakses menggunakan alamat https://semeruyyy.pw/index.php/home -> `https://semerua05.pw/index.php/home` kemudian url di mod rewrite menjadi https://semeruyyy.pw/home -> `https://semerua05.pw/home`

10. Web https://penanjakan.semeruyyy.pw -> `https://penanjakan.semerua05.pw` digunakan untuk menyimpan assets file yang memiliki DocumentRoot pada /var/www/penanjakan.semeruyyy.pw -> `/var/www/penanjakan.semerua05.pw` dan memiliki folder sebagai berikut.

```
/var/www/penanjakan.semeruyyy.pw
                                /public/javascripts
                                /public/css
                                /public/images
                                /errors
```

11. Pada folder `/public` dibolehkan directory listing namun untuk folder didalamnya tidak boleh

12. Mengatasi HTTP Error code 404 disediakan file `404.html` pada folder `/errors`

13. Untuk mengakses file assets javascript yang awalnya menggunakan url https://penanjakan.semeruyyy.pw/public/javascripts -> `https://penanjakan.semerua05.pw/public/javascripts` kemudian url di mod rewrite menjadi https://penanjakan.semeruyyy.pw/js -> `https://penanjakan.semerua05.pw/js`

14. Web https://naik.gunung.semeruyyy.pw -> `https://naik.gunung.semerua05.pw` sudah bisa diakses hanya dengan port 8888

15. Karena https://naik.gunung.semeruyyy.pw -> `https://naik.gunung.semerua05.pw` private, selanjutnya membuat autentifikasi dengan username `semeru` dan password `kuynaikgunung` agar aman dan tidak sembarang orang mengaksesnya

16. IP PROBOLINGGO dialihkan secara otomatis ke https://semeruyyy.pw -> `https://semerua05.pw`

17. Karena pengunjung pada /var/www/penanjakan.semeruyyy.pw/public/images -> `/var/www/penanjakan.semerua05.pw/public/images` sangat banyak maka request gambar yang memiliki substring `semeru` akan diarahkan menuju semeru.jpg
