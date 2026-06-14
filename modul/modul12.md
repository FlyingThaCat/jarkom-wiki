---
title: Modul 12
description: 
published: true
date: 2026-06-14T09:31:18.852Z
tags: 
editor: markdown
dateCreated: 2026-06-14T09:23:52.016Z
---

# Modul 12 ICMP
Internet Control Message Protocol (ICMP) merupakan protokol jaringan yang digunakan untuk mengirimkan informasi terkait kondisi jaringan, pelaporan kesalahan, serta mengecek hubungan antar host.

Beberapa tool jaringan yang menggunakan ICMP antara lain:

- Ping, digunakan untuk menguji apakah suatu host dapat dijangkau melalui jaringan.
- Traceroute (tracert pada Windows), digunakan untuk mengetahui jalur yang dilewati paket menuju host tujuan.

Dalam protokol IP, ICMP menggunakan Protocol Number = 1.

## Analisis ICMP Menggunakan Ping
Kita melakukan capture pada Wireshark kemudian menjalankan perintah:
`ping -n 10 www.ust.hk`
Setelah proses ping selesai, kita lakukan filtering pada Wireshark menggunakan syntax: `icmp`
![12.1.png](/assets/modul12/12.1.png)
Dari hasil capture terlihat terdapat paket ICMP Echo Request dan ICMP Echo Reply. Karena kita mengirim 10 kali ping, maka akan muncul 10 paket request dan 10 paket reply.

Echo Request merupakan paket yang dikirim oleh host pengirim untuk mengecek apakah tujuan dapat dijangkau, sedangkan Echo Reply adalah balasan dari host tujuan yang menandakan bahwa host tersebut aktif.

## Analisis paket ICMP Echo Request
Ketika salah satu paket ICMP dibuka pada Wireshark, terdapat beberapa field penting:
![12.2.png](/assets/modul12/12.2.png)
Type = 8
Menunjukkan bahwa paket merupakan Echo Request.
Code = 0
Tidak ada subkategori khusus untuk Echo Request.
Checksum
Digunakan untuk memverifikasi integritas paket ICMP.
Identifier
Digunakan untuk mencocokkan paket request dengan reply yang sesuai.
Sequence Number
Menunjukkan urutan paket ping yang dikirim.

Selain itu, pada header IP terlihat bahwa Protocol = 1, yang menunjukkan bahwa payload dari paket IP tersebut adalah ICMP.

## Melakukan Traceroute dan analisis ICMP
Kita melakukan capture baru pada Wireshark kemudian menjalankan perintah:
`tracert www.inria.fr` Setelah proses selesai, kita lakukan filtering menggunakan: `icmp`
![12.3.png](/assets/modul12/12.3.png)
Perintah tracert bekerja dengan mengirim paket ICMP menggunakan nilai TTL (Time To Live) yang terus bertambah mulai dari 1.

Setiap router yang menerima paket dengan TTL bernilai 0 akan mengirimkan pesan ICMP Time Exceeded kembali ke pengirim. Dengan cara ini, jalur yang dilewati paket menuju tujuan dapat diketahui.

Pada output traceroute terlihat bahwa untuk setiap hop dikirimkan 3 paket probe, kemudian ditampilkan alamat IP router beserta waktu tempuh (RTT) masing-masing paket.

## Analisis ICMP Time Exceeded
Ketika paket balasan dari router diperiksa pada Wireshark, diperoleh informasi:

![12.4.png](/assets/modul12/12.4.png)

Type = 11
Menunjukkan pesan Time Exceeded.
Code = 0
TTL expired in transit.
Paket ini dikirim oleh router ketika nilai TTL habis sebelum mencapai tujuan.
Paket ICMP Time Exceeded memiliki struktur yang lebih kompleks dibanding Echo Request karena menyertakan sebagian header paket asli sebagai referensi kesalahan.
