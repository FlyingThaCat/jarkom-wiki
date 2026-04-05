---
title: Modul 5 UDP
description: User Datagram Protocol ?
published: true
date: 2026-04-05T18:52:19.026Z
tags: 
editor: markdown
dateCreated: 2026-04-05T18:52:19.026Z
---

# Modul 5 UDP

## Gunakan filter `udp`

![discord.1.png](/assets/modul4/discord.1.png)
Disini saya menggunakan traffic call dari discord. dapat dilihat dari region yang terhubung memiliki `sin` yang mengindikasikan bahwa call kita terhubung ke server discord yang ada di singapura dan dapat dilihat pada ip lookup bahwa ip tersebut merupakan ip datacenter `Linode` yang berlokasi di singapura. dan protokol yang digunakan adalah `STUN` dan `STUN` sendiri menggunakan `UDP` sebagai dasar protokol.

1. Pilih satu paket UDP yang terdapat pada trace Anda. Dari paket tersebut, berapa banyak “field” yang terdapat pada header UDP? Sebutkan nama-nama field yang Anda temukan!
Source Port, Destination Port, Length, and Checksum umumnya adalah `field` header pada UDP dan dibuktikan dengan melihat hasil capture. kita memiliki source port `41641` dan destination port `3478` lalu ada length yang berisikan `48` dan checksum yang berisikan checksum `0xac13`

2. Perhatikan informasi “content field” pada paket yang Anda pilih di pertanyaan 1. Berapa panjang (dalam satuan byte) masing-masing “field” yang terdapat pada header UDP?
Dari data spesifikasi UDP kita dapat mengetahui bahwa panjang field header UDP adalah 8 Byte (FIXED) karena kita mengetahui dan mendapatkan 4 field maka kita hanya perlu membagi 8 Byte / 4 maka kita akan mendapatkan 2. dan UDP memberikan ukuran tetap untuk setiap fieldnya jadi bisa dipastikan setiap field memiliki 2 byte

3. Nilai yang tertera pada ”Length” menyatakan nilai apa? Verfikasi jawaban Anda melalui paket UDP pada trace.
Nilai Length = 48 byte berarti -> Total panjang UDP (header + data/payload). dapat dilihat dari jawaban sebelumnya kita mengetahui total byte untuk header adalah 8 dan panjang payload dari UDP dari capture tersebut adalah 40 maka 40+8 = 48 byte

4. Berapa jumlah maksimum byte yang dapat disertakan dalam payload UDP? (Petunjuk: jawaban untuk pertanyaan ini dapat ditentukan dari jawaban Anda untuk pertanyaan 2)
dapat dilihat pada https://en.wikipedia.org/wiki/User_Datagram_Protocol maksimum payload byte yang dapat dilakukan untuk ipv4 adalah 65,507 bytes

5. Berapa nomor port terbesar yang dapat menjadi port sumber? (Petunjuk: lihat petunjuk pada pertanyaan 4)
https://en.wikipedia.org/wiki/User_Datagram_Protocol dapat dilihat dari artikel yang sama port maximum adalah 16 bit dan 2^16-1 adalah 65535 dan -1 digunakan karena dalam perhitungan octet kita mulai dari 0

6. Berapa nomor protokol untuk UDP? Berikan jawaban Anda dalam notasi heksadesimal dan desimal. Untuk menjawab pertanyaan ini, Anda harus melihat ke bagian ”Protocol” pada datagram IP yang mengandung segmen UDP.
![discord.2.png](/assets/modul4/discord.2.png)
dapat dilihat saat kita mengklik bagian protocol pada Internet Protocol UDP menunjukkan angka `17` yang merupakan notasi desimal dari protocol UDP. dan apabila kita lihat kekanan maka kita dapat melihat angka 11 pada hex view. disini menunjukkan bahwa protocol UDP dinotasikan sebagai 11 / 0x11 pada hex data dari payload jaringan.

7. Periksa pasangan paket UDP di mana host Anda mengirimkan paket UDP pertama dan paket UDP kedua merupakan balasan dari paket UDP yang pertama. (Petunjuk: agar paket kedua merupakan balasan dari paket pertama, pengirim paket pertama harus menjadi tujuan dari paket kedua). Jelaskan hubungan antara nomor port pada kedua paket tersebut!
![discord.3.png](/assets/modul4/discord.3.png)
dari capture tersebut kita dapat melihat dari arah panah terlihat packet sebelum highlight merupakan kita menerima audio dari server discord ke discord client kita diindikasikan dari source yang merupakan ip dari server discord dan destination merupakan ip lokal kita. lalu saat source berubah menjadi ip local kita ke ip discord kita dapat menyimpulkan bahwa pada saat itu discord sedang mengirimkan audio file kita ke server mereka. dan dapat disimpulkan bahwa discord menggunakan port `41641` untuk mengirim data sedangkan discord client menggunakan port `3478` untuk mengirim dan menerima data