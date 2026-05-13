---
title: Modul 11
description: 
published: true
date: 2026-05-13T04:29:00.036Z
tags: 
editor: markdown
dateCreated: 2026-05-13T04:29:00.036Z
---

# Modul 11
1. Apa itu DHCP
	- DHCP (Dynamic Host Configuration Protocol) adalah protokol jaringan yang memberikan konfigurasi IP secara otomatis kepada perangkat yang terhubung ke jaringan. Jadi perangkat tidak perlu setting IP manual — cukup connect ke jaringan, dan DHCP server langsung memberikan IP Address, Subnet Mask, Gateway, dan DNS secara otomatis.
2. Kelebihan dan Kekurangan DHCP
	- Kelebihan:
		- Tidak perlu setting IP manual di setiap perangkat, hemat waktu dan tenaga
		- Menghindari konflik IP karena pemberian IP diatur terpusat oleh server
		- Mudah dikelola, terutama di jaringan dengan banyak perangkat
		- IP yang tidak terpakai bisa didaur ulang dan diberikan ke perangkat lain
	
  - Kekurangan:
		- Jika DHCP server mati, perangkat baru tidak bisa mendapatkan IP
		- IP perangkat bisa berubah-ubah setiap koneksi, kurang cocok untuk server atau perangkat yang butuh IP tetap / static
		- Rentan terhadap serangan seperti DHCP Spoofing, di mana penyerang bisa menyamar jadi DHCP server palsu
3. DORA
	- DORA adalah proses 4 tahap yang terjadi saat perangkat meminta IP ke DHCP server.
		- D — Discover
			- Perangkat baru masuk ke jaringan dan belum punya IP. Ia mengirim broadcast ke seluruh jaringan untuk mencari DHCP server yang tersedia.
		- O — Offer
			-	DHCP server menerima pesan Discover dan membalas dengan menawarkan sebuah IP Address beserta konfigurasi lainnya (subnet, gateway, DNS).
		- R — Request
			- Perangkat menerima tawaran tersebut dan mengirim pesan ke DHCP server untuk mengkonfirmasi bahwa ia menyetujui IP yang ditawarkan.
		- A — Acknowledge
			- DHCP server mengirim konfirmasi akhir, dan IP resmi diberikan ke perangkat. Perangkat sekarang sudah bisa berkomunikasi di jaringan.