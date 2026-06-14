---
title: Modul 14
description: 
published: true
date: 2026-06-14T10:12:04.472Z
tags: 
editor: markdown
dateCreated: 2026-06-14T10:12:04.472Z
---

# Modul 14 802.11 WiFi
## Apa itu 802.11 (WiFi)
IEEE 802.11 merupakan standar komunikasi jaringan nirkabel (Wireless LAN) yang digunakan oleh perangkat WiFi untuk saling terhubung melalui Access Point (AP).

## Jenis frame pada 802.11
- Management Frame → digunakan untuk proses beacon, association, authentication, dan lain-lain.
- Control Frame → digunakan untuk membantu pengiriman data, seperti ACK dan RTS/CTS.
- Data Frame → digunakan untuk membawa payload data pengguna.

## Melakukan capture traffic WiFi
Kita buka Wireshark dan memilih interface WiFi yang sedang digunakan.

![14.1.png](/assets/modul14/14.1.png)

Kemudian kita memulai proses capture sambil melakukan beberapa aktivitas seperti:

- Menghubungkan perangkat ke jaringan WiFi.
- Membuka beberapa website.
- Memutuskan koneksi WiFi lalu menghubungkannya kembali

![14.2.png](/assets/modul14/14.2.png)

Dari hasil capture terlihat adanya berbagai frame yang berkaitan dengan aktivitas jaringan nirkabel.

## Kendala praktikum
Adapter WiFi yang digunakan tidak mendukung monitor mode sehingga frame 802.11 tidak dapat ditangkap secara langsung menggunakan Wireshark.


## Mengamati Beacon Frame
Kita melakukan filtering menggunakan: `wlan.fc.type_subtype == 8`
Beacon Frame merupakan frame management yang dikirim secara berkala oleh Access Point untuk mengumumkan keberadaan jaringan WiFi kepada perangkat di sekitarnya.

![14.3.png](/assets/modul14/14.3.png)

Dari hasil pengamatan pada Wireshark, informasi yang dapat diperoleh dari Beacon Frame antara lain:

- SSID (Service Set Identifier), yaitu nama jaringan WiFi yang dipancarkan oleh Access Point.
- BSSID, yaitu MAC Address milik Access Point.
- Channel, yaitu kanal frekuensi yang digunakan oleh jaringan WiFi.
- Supported Rates, yaitu kecepatan transmisi data yang didukung oleh Access Point.
- Capability Information, yang menunjukkan kemampuan jaringan seperti dukungan privasi (enkripsi) dan fitur lainnya.

Beacon Frame dikirim secara periodik agar perangkat lain dapat mendeteksi keberadaan jaringan WiFi tersebut dan memulai proses koneksi jika diperlukan.

## Mengamati Data Frame
Kita melakukan filtering menggunakan:  `wlan.fc.type == 2`

Data Frame digunakan untuk membawa data pengguna pada jaringan WiFi. Frame ini dapat berisi berbagai jenis payload seperti paket IP, TCP, maupun HTTP.

![14.4.png](/assets/modul14/14.4.png)

Pada hasil capture terlihat adanya pertukaran Data Frame antara client dan Access Point selama proses komunikasi berlangsung. Hal ini menunjukkan bahwa host telah berhasil terhubung ke jaringan nirkabel dan dapat melakukan pertukaran data.

## Mengamati Association dan Disassociation
Association merupakan proses ketika client meminta izin untuk bergabung ke suatu Access Point.

Untuk melihat Association Request, kita dapat menggunakan filter:

`wlan.fc.type_subtype == 0`

![14.5.png](/assets/modul14/14.5.png)

Sedangkan untuk melihat Association Response, digunakan filter:

`wlan.fc.type_subtype == 1`

![14.6.png](/assets/modul14/14.6.png)

Association Request dikirim oleh client menuju Access Point untuk memulai proses koneksi. Setelah itu, Access Point akan mengirimkan Association Response yang berisi status diterima atau ditolaknya permintaan tersebut.

Pada modul ini juga diamati adanya proses perpindahan koneksi, yaitu ketika host mencoba terhubung ke Access Point lain namun gagal, kemudian kembali terhubung ke Access Point sebelumnya.