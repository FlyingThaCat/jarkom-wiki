---
title: Modul 6
description: 
published: true
date: 2026-04-12T15:26:35.791Z
tags: 
editor: markdown
dateCreated: 2026-04-07T12:52:40.505Z
---

# TCP
## 6.3. Tampilan Awal pada Captured Trace
1. Berapa alamat IP dan nomor port TCP yang digunakan oleh komputer klien Anda (sumber) untuk mentransfer ke `gaia.cs.umass.edu`?
- SRC: 192.168.1.7 : 57658
- DST: 128.119.245.12 : 80
![1.png](/assets/modul6/1.png)

## 6.4. Dasar TCP
1. Berapa nomor urut segmen TCP SYN yang digunakan untuk memulai sambungan TCP antara komputer klien dan gaia.cs.umass.edu? Apa yang dimiliki segmen tersebut sehingga teridentifikasi sebagai segmen SYN?
Dari Frame 7 Kenapa ini SYN?
Karena:
Flag: SYN = 1
ACK = 0
Length = 0
yang menyatakan bahwa permintan baru saja dikirim karena client belum mendapatkan ACK
![6.4.1.png](/assets/modul6/6.4.1.png)

2. Berapa nomor urut segmen SYNACK yang dikirim oleh gaia.cs.umass.edu ke komputer klien sebagai balasan dari SYN? Berapa nilai dari field Acknowledgement pada segmen SYNACK? Bagaimana gaia.cs.umass.edu menentukan nilai tersebut? Apa yang dimiliki oleh segmen sehingga teridentifikasi sebagai segmen SYNACK?
Dari Frame 9 kita mendapatkan
Sequence Number = 0
Acknowledgment Number = 1
ACK = Sequence client + 1 = 0 + 1 = 1
Dan dapat dilihat pada gambar kita mendapatkan SYN, ACK pada flags
![6.4.2.png](/assets/modul6/6.4.2.png)

3. Berapa nomor urut segmen TCP yang berisi perintah HTTP POST? Perhatikan bahwa untuk menemukan perintah POST, Anda harus menelusuri content field milik paket di bagian bawah jendela Wireshark, kemudian cari segmen yang berisi "POST" di bagian field DATAnya.
Tidak mungkin dilakukan karena server menggunakan enforced https dan traffic menggunakan TLS 1.3 (HTTPS) sehingga tracing tidak dapat dilakukan dan hanya akan terlihat TLS Handshake saja

4. Anggap segmen TCP yang berisi HTTP POST sebagai segmen pertama dalam koneksi TCP. Berapa nomor urut dari enam segmen pertama dalam TCP (termasuk segmen yang berisi HTTP POST)? Pada jam berapa setiap segmen dikirim? Kapan ACK untuk setiap segmen diterima? Dengan adanya perbedaan antara kapan setiap segmen TCP dikirim dan kapan acknowledgement-nya diterima, berapakah nilai RTT untuk keenam segmen tersebut? Berapa nilai EstimatedRTT setelah penerimaan setiap ACK? (Catatan: Wireshark memiliki fitur yang memungkinkan Anda untuk memplot RTT untuk setiap segmen TCP yang dikirim. Pilih segmen TCP yang dikirim dari klien ke server gaia.cs.umass.edu pada jendela "daftar paket yang ditangkap". Kemudian pilih: Statistics->TCP Stream Graph- >Round Trip Time Graph).
Segmen pertama yang membawa data adalah frame 11 dengan waktu pengiriman 3.011152188 detik dan sequence number 1. ACK terhadap segmen ini diterima pada frame 14 dengan waktu 3.379405215 detik. Selisih waktu antara pengiriman segmen dan penerimaan ACK menghasilkan nilai RTT sebesar sekitar 0.368 detik (368 ms).

5. Berapa panjang setiap enam segmen TCP pertama?
Segmen awal (SYN, SYN-ACK, dan ACK) memiliki panjang 0 byte karena tidak membawa data. Segmen data pertama (frame 11) memiliki panjang 1823 byte, dan segmen berikutnya (frame 16) memiliki panjang 2896 byte. Hal ini menunjukkan bahwa ukuran segmen meningkat ketika mulai membawa data web.

6. Berapa jumlah minimum ruang buffer tersedia yang disarankan kepada penerima dan diterima untuk seluruh trace? Apakah kurangnya ruang buffer penerima pernah menghambat pengiriman?
Nilai window size minimum yang diamati adalah sebesar 64240 byte pada sisi klien. Tidak terdapat indikasi bahwa buffer penerima penuh atau menyebabkan hambatan dalam pengiriman data, karena tidak ditemukan kondisi zero window atau window penuh dalam trace.

7. Apakah ada segmen yang ditransmisikan ulang dalam file trace? Apa yang anda periksa (di dalam file trace) untuk menjawab pertanyaan ini?
Dalam trace terdapat indikasi retransmission yang ditandai oleh Wireshark sebagai “TCP Retransmission” atau “suspected retransmission”. Hal ini dapat dilihat melalui analisis flag TCP pada paket tertentu. Dengan demikian, dapat disimpulkan bahwa terdapat segmen yang ditransmisikan ulang.
![6.4.7.png](/assets/modul6/6.4.7.png)

8. Berapa banyak data yang biasanya diakui oleh penerima dalam ACK? Dapatkah anda mengidentifikasi kasus-kasus di mana penerima melakukan ACK untuk setiap segmen yang diterima?
ACK bersifat cumulative, yaitu mengakui seluruh byte hingga nomor tertentu secara berurutan. Misalnya, ACK 1449 berarti semua byte hingga 1448 telah diterima, dan ACK 1824 berarti data hingga byte 1823 telah diterima. Pada fase awal komunikasi, penerima juga dapat mengirim ACK untuk setiap segmen yang diterima.

9. Berapa throughput (byte yang ditransfer per satuan waktu) untuk sambungan TCP? Jelaskan bagaimana Anda menghitung nilai ini.
Throughput dihitung dengan membagi jumlah data yang ditransfer dengan waktu yang dibutuhkan. Sebagai contoh, segmen dengan ukuran 1823 byte dikirim dalam waktu sekitar 0.368 detik, sehingga throughput diperoleh sekitar 4953 byte per detik atau sekitar 4.95 KB/s.

## 6.5 Congestion Control pada TCP
1. Identifikasi slow start & congestion avoidance
Fase Slow Start Terjadi pada awal grafik (sekitar 0–±5 detik) dengan ciri2:
Grafik melengkung naik tajam
![6.5.1.1.png](/assets/modul6/6.5.1.png)

Fase Congestion Avoidance Terjadi setelah itu (sekitar >5 detik sampai akhir) dengan ciri2:
Grafik mulai lebih lurus (linear)
Kenaikan lebih stabil
Yang memiliki arti:
TCP sudah menemukan kapasitas jaringan
cwnd bertambah perlahan (linear)
![6.5.1.2.png](/assets/modul6/6.5.1.2.png)

2. Perbandingan dengan perilaku ideal TCP
Dibandingkan dengan perilaku ideal TCP, pola yang diamati secara umum sesuai, yaitu adanya fase slow start diikuti congestion avoidance. Namun, grafik hasil pengukuran menunjukkan adanya variasi kecil dan ketidakteraturan, yang disebabkan oleh kondisi jaringan seperti RTT, delayed ACK, dan kemungkinan retransmission.