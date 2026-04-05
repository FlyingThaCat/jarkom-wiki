---
title: Modul 4
description: 
published: true
date: 2026-04-05T18:00:55.481Z
tags: 
editor: markdown
dateCreated: 2026-04-05T17:20:34.207Z
---

# Modul 4 DNS

## 4.2 Nslookup
1. Jalankan nslookup untuk mendapatkan alamat IP dari server web di Asia. Berapa alamat IP server tersebut?
![4.2.1.1.png](/assets/modul4/4.2.1.1.png)
Disini saya melakukan nslookup atau mencari info tentang domain `suro.ubaya.ac.id` dan dapat dilihat permintaan lookup saya diberikan oleh alamat `127.0.2.2` yang berasal dari cloudflare warp yang sedang saya gunakan. Bisa di cek dari screenshot dibawah 
![4.2.1.2.png](/assets/modul4/4.2.1.2.png)
&nbsp;
&nbsp;
2. Jalankan nslookup agar dapat mengetahui server DNS otoritatif untuk universitas di Eropa.
![4.2.2.png](/assets/modul4/4.2.2.png)
Dari gambar diatas dapat dilihat untuk domain dari `Technische Universität München` adalah `tum.de` dan saat kita lakukan request lookup Nameserver / Authoritative DNS dari kampus tersebut didapatkan 3 dns.
&nbsp;
&nbsp;
3. Jalankan nslookup untuk mencari tahu informasi mengenai server email dari Yahoo! Mail melalui salah satu server yang didapatkan di pertanyaan nomor 2. Apa alamat IP-nya?
![4.2.3.1.png](/assets/modul4/4.2.3.1.png)
Jita lakukan lookup untuk Mail Exchange server dari `yahoo.com` dengan menggunakan command diatas dan dari screenshot diatas kita dapat melihat bahwa `yahoo.com` memiliki 3 domain mailserver.
![4.2.3.2.png](/assets/modul4/4.2.3.2.png)
Namun saat kita melakukan lookup ip dari mailserver yahoo.com dengan menggunakan Authoritative DNS dari `tum.de` kita mendapati bahwa semua Authoritative DNS Mereject request lookup kita. dapat disimpulkan bahwa kampus tersebut hanya menggunakan Authoritative DNS mereka untuk mapping internal domain mereka atau domain dari kampus mereka sendiri.
![4.2.3.3.png](/assets/modul4/4.2.3.3.png)
Dapat dibuktikaan dari screenshot diatas saat kita melakukan lookup ip server dari `mta6.am0.yahoodns.net` dengan menggunakan public DNS seperti Quad9 kita mendapatkan result kembali yang menyatakan dari satu domain tersebut terdapat 8 ip server untuk menghandle pengiriman pesan. 
&nbsp;
&nbsp;
## 4.3 ipconfig
![4.3.1.png](/assets/modul4/4.3.1.png)
Untuk melihat ip address kita, kita dapat menggunakan `ipconfig /all` pada windows tetapi karena saya menggunakan linux. cara mengecek ip kita adalah dengan menggunakan command `ip a` dan dapat dilihat pada `wlan0` ip dari wifi saya adalah `172.xxx.xxx.204`
![4.3.2.png](/assets/modul4/4.3.2.png)
Lalu untuk mengecek dns yang sedang digunakan dari sistem kita menggunakan command `resolvectl status` berbeda dari windows yang menggunakan command `ipconfig /displaydns` dan dapat dilihat pada global current dns yang sedang digunakan adalah `127.0.2.2` yang dimana ip tersebut adalah dns dari Cloudflare Warp yang sedang saya gunakan 
![4.3.3.png](/assets/modul4/4.3.3.png)
lalu untuk reset dns cache linux juga menggunakan command yang berbeda yaitu `sudo resolvectl flush-caches` dapat dilihat dari current cache size yang berubah dari `37` menjadi `0` yang menandakan reset dari dns cache laptop kita sukses
&nbsp;
&nbsp;
## 4.4 Tracing DNS dengan Wireshark
### www.ietf.org
&nbsp;
1
![4.4.1.1.png](/assets/modul4/4.4.1.1.png)
2
![4.4.1.2.png](/assets/modul4/4.4.1.2.png)
3
![4.4.2.1.png](/assets/modul4/4.4.2.1.png)
4
![4.4.2.2.png](/assets/modul4/4.4.2.2.png)

1. Cari pesan permintaan DNS dan balasannya. Apakah pesan tersebut dikirimkan melalui UDP atau TCP?
Kita lakukan filtering dengan constraint `laptop kita`, `dns request`, dan memiliki kata `ietf` (foto 1)
Dapat kita lihat dari capture wireshark ke (foto 2), lalu lihat pada panah dikatakan bahwa ada kalimat `User Datagram Protocol` / disingkat menjadi `UDP` dan `Dst Port: 53` yang mengindikasikan bahwa request dns tersebut menggunakan protokol `UDP` dan port `53` adalah port yang digunakan untuk DNS.

2. Apa port tujuan pada pesan permintaan DNS? Apa port sumber pada pesan balasannya?
Dari permintaan domain `www.ietf.org` kita dapat melihat browser melakukan request dari port `57728` ke port `53` (foto 3)
Dan dapat dilihat dari (foto 4) request dikembalikan dari port `53` kembali ke `57728`

3. Pada pesan permintaan DNS, apa alamat IP tujuannya? Apa alamat IP server DNS lokal anda (gunakan ipconfig untuk mencari tahu)? Apakah kedua alamat IP tersebut sama?
ya sama dapat dilihat pada (foto 3) dan (foto di 4.3 bagian wlan0) ip tujuan diarahkan ke DNS lokal dengan akhiran .4 dan dapat dilihat pada wlan0 juga .4 

4. Periksa pesan permintaan DNS. Apa “jenis” atau ”type” dari pesan tersebut? Apakah pesan permintaan tersebut mengandung ”jawaban” atau ”answers”?
dari (foto 3) kita dapat melihat permintaan tsb merupakan query atau penerimaan dan pada (foto 4) merupakan response / jawaban dari permintaan DNS tersebut

5. Periksa pesan balasan DNS. Berapa banyak ”jawaban” atau ”answers” yang terdapat di dalamnya? Apa saja isi yang terkandung dalam setiap jawaban tersebut?
![4.4.5.png](/assets/modul4/4.4.5.png)
dari balasan atau response dns yang ada di (foto 4) kita dapat melihat dns mengembalikan 2 jawaban. yang berisikan bahwa domain `www.ietf.org` memiliki 2 server. yaitu `104.16.45.99` dan `104.16.44.99`

6. Perhatikan paket TCP SYN yang selanjutnya dikirimkan oleh host Anda. Apakah alamat IP pada paket tersebut sesuai dengan alamat IP yang tertera pada pesan balasan DNS?
![4.4.6.png](/assets/modul4/4.4.6.png)
dapat dilihat dari request dns kita mendapat alamat `104.16.44.99` ip untuk `www.ietf.org` dan saat halaman loading / diakses browser kita menghubungi address / alamat server tersebut. sehingga sesuai dengan balasan dns

7. Halaman web yang sebelumnya anda akses (http://www.ietf.org) memuat beberapa gambar. Apakah host Anda perlu mengirimkan pesan permintaan DNS baru setiap kali ingin mengakses suatu gambar?
![4.4.7.png](/assets/modul4/4.4.7.png)
dapat dilihat bahwa `http://www.ietf.org` mengirimkan content image melalui https dan menggunakan domain yang sama sehingga dns tidak perlu dipanggil lagi karena konten yang dibutuhkan sudah berada di server yang sama. dapat dilihat untuk content request dilakukaan ke ip `104.16.45.99` sayangnya kita tidak dapat melakukan sniffing packet dikarenakan content di deliver menggunakan protocol https
&nbsp;
&nbsp;
### nslookup mit.edu
1. Apa port tujuan pada pesan permintaan DNS? Apa port sumber pada pesan balasan DNS?
![mit.1.png](/assets/modul4/mit.1.png)
Dari SS diatas kita dapat lihat port tujuan adalah `53` port sumber adalah `53390` 

2. Ke alamat IP manakah pesan permintaan DNS dikirimkan? Apakah alamat IP tersebut merupakan default alamat IP server DNS lokal Anda?
![mit.1.png](/assets/modul4/mit.1.png)
Permintaan DNS dikirimkan ke `1.1.1.1` dan alamat tersebut merupakan default dns dari laptop saya

3. Periksa pesan permintaan DNS. Apa ”jenis” atau ”type” dari pesan tersebut? Apakah pesan tersebut mengandung ”jawaban” atau ”answers”?
![mit.2.png](/assets/modul4/mit.2.png)
Dari permintaan dns tersebut jenis dari request tersebut adalah `Queries` dan tidak mengandung jawaban

4. Periksa pesan balasan DNS. Berapa banyak ”jawaban” atau “answers” yang terdapat di dalamnya. Apa saja isi yang terkandung dalam setiap jawaban tersebut?
![mit.3.png](/assets/modul4/mit.3.png)
dari gambar diatas dapat dilihat bahwa permintaan tersebut mengembalikan 1 jawaban dan pada jawaban tersebut mengatakan bahwa `A` record dari `mit.edu` memiliki 1 server utama yang memiliki address `104.68.37.236`
&nbsp;
&nbsp;
### nslookup –type=NS mit.edu
1. Ke alamat IP manakah pesan permintaan DNS dikirimkan? Apakah alamat IP tersebut merupakan default alamat IP server DNS lokal Anda?
![mit.ns.1.png](/assets/modul4/mit.ns.1.png)
Permintaan DNS dikirimkan ke `1.1.1.1` dan alamat tersebut merupakan default dns dari laptop saya

2. Periksa pesan permintaan DNS. Apa ”jenis” atau ”type” dari pesan tersebut? Apakah pesan tersebut mengandung ”jawaban” atau ”answers”?
![mit.ns.1.png](/assets/modul4/mit.ns.1.png)
Dari permintaan dns tersebut jenis dari request tersebut adalah `Queries` dan tidak mengandung jawaban perbedaaan yang terlihat perbedaan adalah `Query Type` yang diminta adalah `NS`

3. Periksa pesan balasan DNS. Apa nama server MIT yang diberikan oleh pesan balasan? Apakah pesan balasan ini juga memberikan alamat IP untuk server MIT tersebut?
![mit.ns.2.png](/assets/modul4/mit.ns.2.png)
Dapat dilihat pada jawaban dari dns. dia hanya mengembalikan `Nameserver` dan tidak memberikan ip dari server tersebut

### nslookup www.aiit.or.kr bitsy.mit.edu
1. Ke alamat IP manakah pesan permintaan DNS dikirimkan? Apakah alamat IP tersebut merupakan default alamat IP server DNS lokal Anda?
![bitsy.1.png](/assets/modul4/bitsy.1.png)
Permintaan DNS dikirimkan ke `1.1.1.1` dan alamat tersebut merupakan default dns dari laptop saya

2. Periksa pesan permintaan DNS. Apa ”jenis” atau ”type” dari pesan tersebut? Apakah pesan tersebut mengandung ”jawaban” atau ”answers”?
![bitsy.2.png](/assets/modul4/bitsy.2.png)
Dari permintaan dns tersebut jenis dari request tersebut adalah `Queries` dan tidak mengandung jawaban


3. Periksa pesan balasan DNS. Berapa banyak ”jawaban” atau “answers” yang terdapat di dalamnya. Apa saja isi yang terkandung dalam setiap jawaban tersebut?
![bitsy.3.png](/assets/modul4/bitsy.3.png)
Dapat dilihat dari screenshot sebelumnya tidak ada panah yang menunjukan request dan response yang menandakan bahwa `bitsy.mit.edu` mereject request nslookup kita. dapat dibuktikan dengan munculnya error di terminal. Kemungkinan domain `bitsy.mit.edu` tidak lagi menjadi dns server
