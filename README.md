# Ereshkigal

![Ereshkigal](icon.png)

## Lisensi
**Lisensi:** GPLv3

## Deskripsi Aplikasi
Ereshkigal adalah aplikasi pengujian injeksi paket (deauther) WiFi yang dirancang untuk digunakan dengan modul RTL8720DN. Aplikasi ini memberikan pengguna kemampuan untuk menguji jaringan WiFi dengan melakukan serangan deauthentication dan mengidentifikasi titik akses yang lemah.

## Fitur Aplikasi
- Injeksi paket deauthentication untuk menguji keamanan jaringan WiFi.
- Antarmuka pengguna yang sederhana dan intuitif.
- Kompatibilitas dengan modul RTL8720DN (AI-Thinker BW16).
- Mendukung injeksi paket deauthentication pada jaringan 2.4Ghz dan 5Ghz
- Proses flashing yang mudah dengan Ereshkigal Flasher.

## Bahan-bahan yang Dibutuhkan
- Modul RTL8720DN (AI-Thinker BW16)
- Kabel USB Tipe C untuk koneksi antara modul dan komputer
- Komputer dengan sistem operasi Windows
- Ereshkigal.bin (file binary aplikasi)
- Ereshkigal Flasher V1.0.0.exe (aplikasi untuk flashing)

## Cara Flashing
1. Hubungkan modul RTL8720DN ke komputer menggunakan kabel USB Tipe C.
2. Unduh dan jalankan `Ereshkigal Flasher V1.0.0.exe`.
3. Pilih file `Ereshkigal.bin` yang telah Anda unduh sebelumnya.
4. Klik tombol "Start Flash" untuk memulai proses flashing.
5. Tunggu hingga proses flashing selesai. Modul akan reboot secara otomatis.

## Cara Penggunaan
1. Setelah flashing selesai, sambungkan modul ke sumber daya.
2. Buka jaringan WiFi anda maka anda akan menemukan SSID dengan nama `Ereshkigal`
3. Password `Ereshkigal` adalah `masukangin`
4. Setelah terkoneksi dengan Ereshkigal, buka alamat IP `192.168.1.1`
5. Pilih jaringan WiFi yang ingin Anda uji dengan mencentang jaringan.
6. Tekan tombol "Serang" untuk memulai pengujian.
7. Gunakan tombol "Scan" untuk melakukan pemindaian ulang jaringan.
8. Gunakan tombol "Stop" untuk menghentikan pengujian.

---

**Catatan:** Pastikan untuk menggunakan aplikasi ini hanya untuk tujuan pengujian jaringan pribadi dan sesuai dengan hukum yang berlaku.
