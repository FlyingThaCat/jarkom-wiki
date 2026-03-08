---
title: Modul 1
description: Instalasi Wireshark Pada Ubuntu 25.10
published: true
date: 2026-03-08T15:40:33.622Z
tags: 
editor: markdown
dateCreated: 2026-03-08T15:16:42.029Z
---

# Instalasi Wireshark Pada Ubuntu 25.10
Wireshark adalah penganalisis paket bebas dan sumber terbuka. Perangkat ini digunakan untuk pemecahan masalah jaringan, analisis, perangkat lunak dan pengembangan protokol komunikasi, dan pendidikan. Awalnya bernama Ethereal, pada Mei 2006 proyek ini berganti nama menjadi Wireshark karena masalah merek dagang. [Wikipedia](https://id.wikipedia.org/wiki/Wireshark)

## Prerequites
- Ubuntu
- Sudo / Root Account
- Internet

## Langkah - Langkah
1. Buka Terminal Dengan Menekan `CTRL + ALT + T`
2. Selanjutnya Ketikkan `sudo apt install wireshark -y` Dan Masukkan Password Jika Diminta
3. Pada Menu Ini Pilih `Yes` Dan **enter**
![1.png](/assets/modul1/1.png)
4. Restart Laptop
5. Buka Wireshark Pada App Launcher
![2.png](/assets/modul1/2.png)
6. Lakukan Uji Capture Dengan Memilih WIFI Interface Pada Wireshark
![3.png](/assets/modul1/3.png)
7. Apabila Sudah Terlihat Traffic Seperti Dibawah Maka Pemasangan Wireshark Berhasil
![4.png](/assets/modul1/4.png)
8. Buka URL `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.html` Pada Incognito mode
![4.png](/assets/modul2/4.png)
9. Ubah HTTPS menjadi HTTP
![5.png](/assets/modul2/5.png)
Dan Pastikan Muncul Not Secure Seperti Dibawah
![6.png](/assets/modul2/6.png)
10. Cek Pada Wireshark Dan Cari Kalimat `GET /wireshark-labs/HTTP-wireshark-file1.html` Dan Double Klik Pada Response In Frame
![7.png](/assets/modul2/7.png)
11. Lalu Klik Pada `Line-based text data`
![8.png](/assets/modul2/8.png)
12. Amati Response
![9.png](/assets/modul2/9.png)
13. Lalu Buka URL Ini `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html` Pada Incognito Dan Pastikan Sudah Diakses Menjadi HTTP
![10.png](/assets/modul2/10.png)
14. Amati Wireshark
![11.png](/assets/modul2/11.png)

## Kesimpulan
Dari Percobaan Diatas Kita Dapat Menyimpulkan Saat Client Mengakses Url. Client Akan Melakukan Handshake Kepada Server, Lalu Server Menjawab Kembali Dengan Mengirimkan Response `200 OK` Lalu Apabila Ditemukan Image Maupun Aset Lainnya Maka Client Akan Merequest Asset Tersebut Ke Server Sebelum Menampilkannya Ke Client