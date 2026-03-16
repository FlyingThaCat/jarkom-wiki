---
title: Modul 3
description: Analisis HTTP Packet
published: true
date: 2026-03-16T14:30:50.740Z
tags: 
editor: markdown
dateCreated: 2026-03-16T14:30:50.739Z
---

# Analisis HTTP Packet
Kegiatan ini bertujuan untuk menangkap dan menganalisis lalu lintas HTTP pada jaringan menggunakan Wireshark. Melalui proses capture paket, pengguna dapat melihat bagaimana data HTTP dikirim antara client dan server serta memahami struktur dan isi paket yang ditransmisikan di jaringan.

## Prerequites
- Linux
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
4. Buka URL `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file3.html` Pada Incognito mode
Dan Pastikan Muncul Not Secure Seperti Dibawah
![4.png](/assets/modul3/4.png)
5. Amati Response Dapat Dilihat Hasil Response Merupakan Raw File Dari HTML Sebelumnya
![5n.png](/assets/modul3/5n.png)
6. Lalu Buka URL Ini `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html` Pada Incognito Dan Pastikan Sudah Diakses Menjadi HTTP
![10.png](/assets/modul2/10.png)
7. Amati Wireshark
![11.png](/assets/modul2/11.png)
8. Lalu Buka URL Ini `http://gaia.cs.umass.edu/wireshark-labs/protected_pages/HTTP-wireshark-file5.html` Pada Incognito Dan Pastikan Sudah Diakses Menjadi HTTP Dan Pastikan Muncul Seperti Ini
![8.png](/assets/modul3/8.png)
9. Masukkan Username `wireshark-students` Dan Password `network` dan klik Sign In
![9.png](/assets/modul3/9.png)
Pastikan Muncul Seperti Dibawah
![10.png](/assets/modul3/10.png)
10. Lalu Cek Pada Wireshark Dapat Dilihat Password Dan Username Terlihat Bebas Pada Capture
![11.png](/assets/modul3/11.png)


## Kesimpulan
Dari Percobaan Diatas Kita Dapat Menyimpulkan Saat Client Mengakses Url. Client Akan Melakukan Handshake Kepada Server, Lalu Server Menjawab Kembali Dengan Mengirimkan Response `200 OK` Dan Dapat Dilihat Pada Capture Terakhir Koneksi HTTP Tidak Melakukan Enkripsi Sehingga Kita Dapat Melihat Data Apa Saja Yang Client Kirim Ke Server Termasuk Password