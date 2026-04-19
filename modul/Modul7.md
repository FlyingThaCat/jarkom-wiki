---
title: Modul 7
description: 
published: true
date: 2026-05-12T13:23:30.682Z
tags: 
editor: markdown
dateCreated: 2026-05-12T12:52:54.078Z
---

# Modul 7 - SOCKET PROGRAMMING
1. Untuk modul ini buatlah virtualenv pada folder seperti dibawah
![1.png](/assets/modul7/1.png)
untuk membuat virtual environment baru kita ketik command diatas
![1.2.png](/assets/modul7/1.2.png)
lalu aktifkan virtual environment baru kita ketik command diatas dan apabila sukses maka akan ditunjukkan dengan munculnya venv pada awal input

Untuk code akan dijelaskan secara line by line melalui comment
# UDP
![udp.client.png](/assets/modul7/udp.client.png)
![udp.server.png](/assets/modul7/udp.server.png)
![udp.res.png](/assets/modul7/udp.res.png)

# TCP
![tcp.client.png](/assets/modul7/tcp.client.png)
![tcp.server.png](/assets/modul7/tcp.server.png)
![tcp.res.png](/assets/modul7/tcp.res.png)

Dari hasil percobaan tersebut dapat dilihat bahwa komunikasi antara client dan server berhasil dilakukan menggunakan metode socket programming dengan protokol UDP dan TCP. Pada bagian UDP, client mengirim pesan ke server tanpa perlu membuat koneksi terlebih dahulu, lalu server menerima pesan tersebut dan mengirimkan balasan berupa teks yang sudah diubah menjadi huruf kapital. Hal ini menunjukkan bahwa UDP bekerja lebih sederhana dan cepat karena komunikasi berlangsung secara connectionless.

Sedangkan pada bagian TCP, sebelum proses pengiriman data dilakukan, client harus terlebih dahulu terhubung ke server menggunakan koneksi TCP. Setelah koneksi berhasil dibuat, client dapat mengirim pesan dan server membalas pesan tersebut setelah dimodifikasi menjadi huruf kapital. Dari hasil tersebut dapat disimpulkan bahwa TCP menggunakan mekanisme koneksi yang lebih terstruktur dibanding UDP sehingga komunikasi data menjadi lebih stabil dan terjamin diterima oleh client.