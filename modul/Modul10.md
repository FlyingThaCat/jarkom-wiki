---
title: Modul 10
description: 
published: true
date: 2026-05-13T04:15:19.217Z
tags: 
editor: markdown
dateCreated: 2026-05-13T04:15:19.217Z
---

# Modul 10
- Apa itu IP Address
1. IP Address adalah alamat unik yang diberikan kepada setiap perangkat yang terhubung ke jaringan, agar perangkat-perangkat tersebut bisa saling mengenali dan berkomunikasi satu sama lain, seperti alamat rumah di dunia nyata.
- Traceroute dari suatu website

![traceroute.png](/assets/modul10/traceroute.png)

Ketika perintah `traceroute x.com` dijalankan, komputer mengirim paket ke `x.com (IP 162.159.140.229)` sambil mencatat setiap router yang dilewati di sepanjang jalur.
Paket pertama kali keluar melalui router lokal di `172.16.10.1`, kemudian masuk ke jaringan ISP di `10.45.0.1`. Pada hop ke-3 muncul 3 IP berbeda, hal ini terjadi karena ISP menggunakan load balancing, sehingga setiap percobaan paket bisa melewati jalur yang berbeda.
Di hop ke-5 terdapat tanda `*`, yang berarti salah satu paket tidak mendapat balasan karena router tersebut memblokir ICMP. Pada hop yang sama, paket sudah mulai masuk ke jaringan Cloudflare.
Akhirnya di hop ke-7, paket berhasil sampai ke server x.com. Dengan total 7 hop dan latency sekitar 17–19 ms, jalur ini tergolong pendek dan efisien. Range IP yang muncul (162.158.x.x dan 162.159.x.x) menunjukkan bahwa x.com menggunakan infrastruktur Cloudflare.

- Apa itu ICMP, MTU, TTL
1. ICMP (Internet Control Message Protocol) — protokol untuk mengirim pesan error dan informasi jaringan. Contoh penggunaan pada perintah ping dan traceroute.
2. MTU (Maximum Transmission Unit) — ukuran maksimal paket data yang bisa dikirim dalam satu transmisi. Biasanya 1500 bytes di jaringan Ethernet.
3. TTL (Time To Live) — nilai hitungan yang menentukan berapa lama/banyak hop sebuah paket boleh melewati router sebelum dibuang, untuk mencegah paket berputar selamanya di jaringan.

- Cari suatu fragmentasi di wireshark

![fragment.png](/assets/modul10/fragment.png)

kita lakukan filter dengan menggunakan syntax
`ip.flags.mf == 1 || ip.frag_offset > 0` 
`ip.flags.mf == 1` → menangkap paket yang masih ada fragmen lanjutannya (More Fragments)
`ip.frag_offset > 0` → menangkap fragmen kedua dan seterusnya

lalu kita lakukan force ping dengan mengirimkan ping dengan data yang melebihi MTU dengan menggunakan `ping -s 3000 x.com` Paket sebesar 3000 bytes akan melebihi MTU 1500 bytes, sehingga akan dipecah dan fragmentasi akan muncul di Wireshark.

- Carilah IPV6 di wireshark yang kalian lakukan

![ipv6.png](/assets/modul10/ipv6.png)

Kita gunakan vpn untuk mendapat ipv6 dan kita lakukan filtering untuk ipv6 dan kita lakukan ping ke salah satu website yang menyediakan ipv6 seperti `ipv6.google.com` 