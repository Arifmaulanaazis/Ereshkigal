<h1 align="center">Ereshkigal</h1>

<p align="center">
  <img src="icon.png" alt="Ereshkigal Icon" width="300" height="300" style="object-fit: cover;">
</p>

<p align="center">
  <a href="https://hits.seeyoufarm.com"><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FArifmaulanaazis%2FEreshkigal&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=Total+Viewer&edge_flat=false"/></a>
  <img src="https://img.shields.io/github/downloads/Arifmaulanaazis/Ereshkigal/total?style=flat-square" alt="GitHub downloads"/>
</p>

<h2 align="center">Lisensi</h2>
<p align="center"><strong>Lisensi:</strong> GPLv3</p>

## Pilih Bahasa / Select Language / Chọn Ngôn Ngữ / เลือกภาษา / 言語を選択
- [Indonesia](README.md)
- [English](README-English.md)
- [Vietnamese](README-Vietnam.md)
- [Thailand](README-Thailand.md)
- [Japanese](README-Japanese.md)


## Deskripsi Aplikasi
Ereshkigal adalah aplikasi pengujian injeksi paket (deauther) WiFi yang dirancang untuk digunakan dengan modul RTL8720DN. Aplikasi ini memberikan pengguna kemampuan untuk menguji jaringan WiFi dengan melakukan serangan deauthentication dan mengidentifikasi titik akses yang lemah.

## Fitur Aplikasi
- Injeksi paket deauthentication untuk menguji keamanan jaringan WiFi.
- Antarmuka pengguna yang sederhana dan intuitif.
- Kompatibilitas dengan modul RTL8720DN (AI-Thinker BW16).
- Mendukung injeksi paket deauthentication pada jaringan 2.4Ghz dan 5Ghz
- Proses flashing yang mudah dengan Ereshkigal Flasher.

## Bahan-bahan yang Dibutuhkan
- Modul RTL8720DN (AI-Thinker BW16) [Saya belinya di sini](https://tokopedia.link/1k7qXB2VENb).
- Kabel USB Tipe C untuk koneksi antara modul dan komputer
- Komputer dengan sistem operasi Windows
- Ereshkigal V1.0.3 <Target-Bahasa>.bin (file binary aplikasi)
- Ereshkigal Flasher V1.0.0.exe (aplikasi untuk flashing)

## Video Tutorial Instalasi dan Pemakaian
Untuk tutorial instalasi dan pemakaian, silakan tonton video di [YouTube](https://youtu.be/r1fH1nWJnAg).

## Cara Flashing
1. Hubungkan modul RTL8720DN ke komputer menggunakan kabel USB Tipe C.
2. Unduh dan jalankan `Ereshkigal Flasher V1.0.0.exe`.
3. Pilih file `Ereshkigal V1.0.3 <Target-Bahasa>.bin` yang telah Anda unduh sebelumnya.
4. Klik tombol "Start Flash" untuk memulai proses flashing.
5. Tunggu hingga proses flashing selesai. Modul akan reboot secara otomatis.

## Cara Penggunaan
1. Setelah flashing selesai, sambungkan modul ke sumber daya.
2. Buka jaringan WiFi anda maka anda akan menemukan SSID dengan nama `Ereshkigal`
3. Password `Ereshkigal` adalah `masukangin`
4. Setelah terkoneksi dengan Ereshkigal, buka alamat IP `192.168.1.1`
5. Pilih jaringan WiFi yang ingin Anda uji dengan mencentang jaringan.
6. Tekan tombol "Deauth" untuk memulai pengujian.
7. Gunakan tombol "Scan" untuk melakukan pemindaian ulang jaringan.
8. Gunakan tombol "RST" pada RTL8720DN untuk menghentikan pengujian.

---

**Catatan:** Pastikan untuk menggunakan aplikasi ini hanya untuk tujuan pengujian jaringan pribadi dan sesuai dengan hukum yang berlaku.
