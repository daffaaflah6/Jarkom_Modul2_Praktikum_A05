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

![1a](https://user-images.githubusercontent.com/52326074/98806455-d1722d00-244b-11eb-9621-c02f013a4686.png)

![1b](https://user-images.githubusercontent.com/52326074/98806448-cf0fd300-244b-11eb-87f7-65281be58728.png)

![1c](https://user-images.githubusercontent.com/52326074/98806707-2dd54c80-244c-11eb-92ca-6e446e3d45d3.jpg)

2. Alias https://www.semeruyyy.pw -> ` https://www.semerua05.pw`

![2a](https://user-images.githubusercontent.com/52326074/98806902-768d0580-244c-11eb-96b3-6df87da382a9.jpg)

![2b](https://user-images.githubusercontent.com/52326074/98806897-74c34200-244c-11eb-932d-765a4fff0f4d.jpg)

![2c](https://user-images.githubusercontent.com/52326074/98806900-75f46f00-244c-11eb-917d-71c42a3511c7.jpg)

3. Subdomain https://penanjakan.semeruyyy.pw -> `https://penanjakan.semerua05.pw`

![3a](https://user-images.githubusercontent.com/52326074/98807682-9a048000-244d-11eb-9266-46c0f42c2f07.jpg)

![3b](https://user-images.githubusercontent.com/52326074/98807686-9bce4380-244d-11eb-948f-a22d17fbf876.jpg)

4. Reverse domain untuk domain utama

![4](https://user-images.githubusercontent.com/52326074/98808134-45add000-244e-11eb-8662-801a95b65821.jpg)

5. DNS Slave pada MOJOKETO

![5a](https://user-images.githubusercontent.com/52326074/98808484-c371db80-244e-11eb-9847-549dce310244.png)

![5b](https://user-images.githubusercontent.com/52326074/98808476-c076eb00-244e-11eb-9400-f85c44339ea1.jpg)

![5c](https://user-images.githubusercontent.com/52326074/98808477-c1a81800-244e-11eb-8a08-7b8c3b01df59.jpg)

![5d](https://user-images.githubusercontent.com/52326074/98808479-c240ae80-244e-11eb-9438-98b058368f6c.jpg)

6. Subdomain dengan alamat https://gunung.semeruyyy.pw -> `https://gunung.semerua05.pw` yang didelegasikan pada server MOJOKERTO dan mengarahkan ke IP PROBOLINGGO

![6a](https://user-images.githubusercontent.com/52326074/98809038-95d96200-244f-11eb-93cc-88f65ef1b313.jpg)

![6b](https://user-images.githubusercontent.com/52326074/98809026-93770800-244f-11eb-86a4-843468b2421d.jpg)

![6c7b](https://user-images.githubusercontent.com/52326074/98809033-94a83500-244f-11eb-8346-f7c8fdf0b6c7.jpg)

7. Subdomain dengan alamat https://naik.gunung.semeruyyy.pw -> `https://naik.gunung.semerua05.pw` domain ini diarahkan ke IP PROBOLINGGO

![7a](https://user-images.githubusercontent.com/52326074/98809174-b86b7b00-244f-11eb-80c8-b12ec168c8b5.jpg)

![6c7b](https://user-images.githubusercontent.com/52326074/98809033-94a83500-244f-11eb-8346-f7c8fdf0b6c7.jpg)

8. Domain https://semeruyyy.pw -> `https://semerua05.pw` memiliki DocumentRoot pada /var/www/semeruyyy.pw -> `/var/www/semerua05.pw`

![8](https://user-images.githubusercontent.com/52326074/98809961-016fff00-2451-11eb-8570-307325054d36.jpg)

9. Awalnya dapat diakses menggunakan alamat https://semeruyyy.pw/index.php/home -> `https://semerua05.pw/index.php/home` kemudian url di mod rewrite menjadi https://semeruyyy.pw/home -> `https://semerua05.pw/home`

![9~](https://user-images.githubusercontent.com/52326074/98810601-0e412280-2452-11eb-8aa0-d457c0a4fb1a.png)

![9](https://user-images.githubusercontent.com/52326074/98809955-ffa63b80-2450-11eb-8188-14a25657dc0c.jpg)

10. Web https://penanjakan.semeruyyy.pw -> `https://penanjakan.semerua05.pw` digunakan untuk menyimpan assets file yang memiliki DocumentRoot pada /var/www/penanjakan.semeruyyy.pw -> `/var/www/penanjakan.semerua05.pw` dan memiliki folder sebagai berikut.

```
/var/www/penanjakan.semeruyyy.pw
                                /public/javascripts
                                /public/css
                                /public/images
                                /errors
```

![1011a](https://user-images.githubusercontent.com/52326074/98816038-a93dfa80-245a-11eb-83eb-d2f1d93cbbec.png)

![1011b](https://user-images.githubusercontent.com/52326074/98816039-a9d69100-245a-11eb-9eb2-cea26b355067.png)

![1011c](https://user-images.githubusercontent.com/52326074/98816025-a4794680-245a-11eb-99fb-f5a3d4b542d9.png)

![1011d](https://user-images.githubusercontent.com/52326074/98816031-a6430a00-245a-11eb-9106-0299b9033efe.jpg)

![1011e](https://user-images.githubusercontent.com/52326074/98816033-a6dba080-245a-11eb-8402-e374aa126b60.jpg)

![10f](https://user-images.githubusercontent.com/52326074/98816035-a80ccd80-245a-11eb-8008-68595b0783c6.jpg)

11. Pada folder `/public` dibolehkan directory listing namun untuk folder didalamnya tidak boleh

![1011a](https://user-images.githubusercontent.com/52326074/98816038-a93dfa80-245a-11eb-83eb-d2f1d93cbbec.png)

![1011b](https://user-images.githubusercontent.com/52326074/98816039-a9d69100-245a-11eb-9eb2-cea26b355067.png)

![1011c](https://user-images.githubusercontent.com/52326074/98816025-a4794680-245a-11eb-99fb-f5a3d4b542d9.png)

![1011d](https://user-images.githubusercontent.com/52326074/98816031-a6430a00-245a-11eb-9106-0299b9033efe.jpg)

![1011e](https://user-images.githubusercontent.com/52326074/98816033-a6dba080-245a-11eb-8402-e374aa126b60.jpg)

12. Mengatasi HTTP Error code 404 disediakan file `404.html` pada folder `/errors`

![12a](https://user-images.githubusercontent.com/52326074/98816275-fe7a0c00-245a-11eb-8aac-daa2b7ed8bc7.jpg)

![12b](https://user-images.githubusercontent.com/52326074/98816266-fc17b200-245a-11eb-9b7f-1e783f6fdf17.png)

![12c](https://user-images.githubusercontent.com/52326074/98816271-fd48df00-245a-11eb-9d0c-83bf81d2662a.jpg)

13. Untuk mengakses file assets javascript yang awalnya menggunakan url https://penanjakan.semeruyyy.pw/public/javascripts -> `https://penanjakan.semerua05.pw/public/javascripts` kemudian url di mod rewrite menjadi https://penanjakan.semeruyyy.pw/js -> `https://penanjakan.semerua05.pw/js`

14. Web https://naik.gunung.semeruyyy.pw -> `https://naik.gunung.semerua05.pw` sudah bisa diakses hanya dengan port 8888

15. Karena https://naik.gunung.semeruyyy.pw -> `https://naik.gunung.semerua05.pw` private, selanjutnya membuat autentifikasi dengan username `semeru` dan password `kuynaikgunung` agar aman dan tidak sembarang orang mengaksesnya

16. IP PROBOLINGGO dialihkan secara otomatis ke https://semeruyyy.pw -> `https://semerua05.pw`

17. Karena pengunjung pada /var/www/penanjakan.semeruyyy.pw/public/images -> `/var/www/penanjakan.semerua05.pw/public/images` sangat banyak maka request gambar yang memiliki substring `semeru` akan diarahkan menuju semeru.jpg
