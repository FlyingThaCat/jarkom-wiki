---
title: Modul 9
description: 
published: true
date: 2026-05-12T14:38:26.373Z
tags: 
editor: markdown
dateCreated: 2026-05-12T14:38:26.373Z
---

# Modul 9 - WEB SERVER
1. Untuk modul ini buatlah virtualenv pada folder seperti dibawah

![1.png](/assets/modul7/1.png)

untuk membuat virtual environment baru kita ketik command diatas

![1.2.png](/assets/modul7/1.2.png)

lalu aktifkan virtual environment baru kita ketik command diatas dan apabila sukses maka akan ditunjukkan dengan munculnya venv pada awal input

Untuk code akan dijelaskan secara line by line melalui comment

## Membuat file not found
Kita buat default page apabila halaman tidak ditemukan dengan membuat file `404.html` yang berisikan kode seperti ini

![404.png](/assets/modul9/404.png)

## Membuat index page / main page
Lalu kita buat halaman utama yang ingin di tampilkan, contoh disini saya membuat file `hallo.html` dengan kode seperti dibawah

![main.png](/assets/modul9/main.png)

## Membuat server
Lalu buatlah file baru yang bernama `server.py` dan ketikkan kode dibawah

![server.png](/assets/modul9/server.png)

Lalu jalankan server seperti gambar dibawah dan pastikan dapat mengakses file

![work.png](/assets/modul9/work.png)

![notfound.png](/assets/modul9/notfound.png)

Dari hasil percobaan tersebut dapat dilihat bahwa server berhasil menjalankan web server sederhana menggunakan socket TCP dan threading. Saat client atau browser mengirim request HTTP, server menerima request tersebut lalu mengambil file HTML yang diminta dan mengirimkannya kembali ke client. Jika file ditemukan maka server mengirim response 200 OK, sedangkan jika file tidak ditemukan server akan mengirim response 404 Not Found beserta halaman error. Penggunaan threading memungkinkan server menangani lebih dari satu client secara bersamaan sehingga komunikasi menjadi lebih efisien dan tidak perlu menunggu client lain selesai terlebih dahulu.