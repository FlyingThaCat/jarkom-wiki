---
title: Modul 13
description: 
published: true
date: 2026-06-14T09:52:31.199Z
tags: 
editor: markdown
dateCreated: 2026-06-14T09:51:57.912Z
---

# Modul 13 Ethernet and ARP
Ethernet merupakan teknologi jaringan pada layer Data Link (Layer 2 OSI) yang digunakan untuk komunikasi antar perangkat dalam satu jaringan lokal (LAN). Ethernet menggunakan MAC Address sebagai identitas unik setiap perangkat.

Beberapa field penting pada Ethernet frame:
- Destination MAC Address → alamat tujuan frame.
- Source MAC Address → alamat pengirim frame.
- Type → menunjukkan jenis payload yang dibawa, misalnya IPv4 (0x0800) atau ARP (0x0806).
- Data → isi frame yang membawa protokol layer atas.
- Frame Check Sequence (FCS) → digunakan untuk mendeteksi error.

## Mengamati frame Ethernet di Wireshark
Kita membersihkan cache browser terlebih dahulu, kemudian melakukan capture menggunakan Wireshark.

Selanjutnya kita buka halaman:
http://gaia.cs.umass.edu/wireshark-labs/HTTP-ethereal-lab-file3.html

Setelah halaman berhasil dimuat, kita menghentikan proses capture.
Kemudian kita mencari paket HTTP GET yang dikirim menuju server.


![13.1.png](/assets/modul13/13.1.png)


Dari hasil capture terlihat adanya paket HTTP GET yang digunakan browser untuk meminta halaman web dari server tujuan.

Selanjutnya kita memilih Analyze → Enabled Protocols, lalu menghilangkan centang pada protokol IP agar hanya protokol layer bawah yang ditampilkan.

![13.2.png](/assets/modul13/13.2.png)

Dari hasil tersebut dapat diamati bahwa frame Ethernet berisi informasi MAC Address pengirim dan penerima yang digunakan untuk komunikasi pada jaringan lokal.

## Apa itu ARP
ARP (Address Resolution Protocol) merupakan protokol yang digunakan untuk menerjemahkan IP Address menjadi MAC Address agar perangkat dapat mengirim frame Ethernet ke tujuan yang benar dalam jaringan lokal.

## Melihat isi ARP Cache
Kita membuka Command Prompt kemudian menjalankan perintah: `arp -a`

![13.3.png](/assets/modul13/13.3.png)

Perintah tersebut digunakan untuk melihat daftar pasangan IP Address dan MAC Address yang tersimpan pada ARP cache.

Setiap entri menunjukkan hasil pemetaan alamat IP ke alamat fisik perangkat yang pernah dihubungi sebelumnya.

## Menghapus ARP Cache
Untuk mengamati proses ARP Request dan ARP Reply, kita perlu menghapus isi cache ARP menggunakan perintah: `arp -d *`

![13.4.png](/assets/modul13/13.4.png)

Perintah tersebut akan menghapus seluruh entri ARP sehingga sistem harus melakukan proses ARP kembali saat ingin mengakses perangkat lain.

## Mengamati proses ARP di Wireshark
Setelah cache ARP dihapus, kita memulai capture Wireshark dan membuka kembali halaman:

http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-lab-file3.html

Kemudian kita melakukan filtering menggunakan: `arp`

![13.5.png](/assets/modul13/13.5.png)

Terlihat adanya dua jenis paket ARP, yaitu:

- ARP Request
Digunakan untuk menanyakan siapa pemilik suatu IP Address.
Bersifat broadcast ke seluruh jaringan lokal.
- ARP Reply
Dikirim oleh perangkat yang memiliki IP Address tersebut.
Berisi MAC Address milik perangkat tersebut.

Sebagai contoh:

"Who has 192.168.1.1? Tell 192.168.1.100"

akan dibalas dengan:

"192.168.1.1 is at xx:xx:xx:xx:xx"