---
title: Modul 2
description: Uji Coba HTTP Capture Menggunakan Wireshark
published: true
date: 2026-03-08T15:47:01.242Z
tags: 
editor: markdown
dateCreated: 2026-03-08T15:47:01.242Z
---

# Uji Coba Capture HTTP Traffic Menggunakan Wireshark
Kegiatan ini bertujuan untuk menangkap dan menganalisis lalu lintas HTTP pada jaringan menggunakan Wireshark. Melalui proses capture paket, pengguna dapat melihat bagaimana data HTTP dikirim antara client dan server serta memahami struktur dan isi paket yang ditransmisikan di jaringan.

## Prerequites
- Ubuntu
- Wireshark
- Sudo / Root Account
- Internet

## Langkah - Langkah
1. Buka Wireshark Pada App Launcher
![2.png](/assets/modul2/1.png)
2. Lakukan Uji Capture Dengan Memilih WIFI Interface Pada Wireshark
![3.png](/assets/modul2/2.png)
3. Apabila Sudah Terlihat Traffic Seperti Dibawah Maka Pemasangan Wireshark Berhasil
![4.png](/assets/modul2/3.png)
4. Buka URL `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.html` Pada Incognito mode
![4.png](/assets/modul2/4.png)
5. Ubah HTTPS menjadi HTTP
![5.png](/assets/modul2/5.png)
Dan Pastikan Muncul Not Secure Seperti Dibawah
![6.png](/assets/modul2/6.png)
6. Cek Pada Wireshark Dan Cari Kalimat `GET /wireshark-labs/HTTP-wireshark-file1.html` Dan Double Klik Pada Response In Frame
![7.png](/assets/modul2/7.png)
7. Lalu Klik Pada `Line-based text data`
![8.png](/assets/modul2/8.png)
8. Amati Response
![9.png](/assets/modul2/9.png)
9. Lalu Buka URL Ini `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html` Pada Incognito Dan Pastikan Sudah Diakses Menjadi HTTP
![10.png](/assets/modul2/10.png)
10. Amati Wireshark
![11.png](/assets/modul2/11.png)

## Kesimpulan
Dari Percobaan Diatas Kita Dapat Menyimpulkan Saat Client Mengakses Url. Client Akan Melakukan Handshake Kepada Server, Lalu Server Menjawab Kembali Dengan Mengirimkan Response `200 OK` Lalu Apabila Ditemukan Image Maupun Aset Lainnya Maka Client Akan Merequest Asset Tersebut Ke Server Sebelum Menampilkannya Ke Client