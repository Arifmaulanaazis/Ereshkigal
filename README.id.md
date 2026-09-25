<div align="center">

<img src="assets/logo.png" width="96" height="96" alt="Ereshkigal">

# Ereshkigal Project

**Flash sekali klik untuk firmware uji-keamanan Wi-Fi Ereshkigal RTL8720DN (BW16).**

Tanpa Arduino IDE. Tanpa source. Tanpa command line. Cukup folder ini.

[English](README.md) · **Bahasa Indonesia** · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [中文](README.zh.md)

![versi](https://img.shields.io/badge/versi-2.0.0-6c4cf1)
![platform](https://img.shields.io/badge/platform-Windows%2010%2F11-2fa565)
![board](https://img.shields.io/badge/board-RTL8720DN%20(BW16)-14161d)
![bahasa](https://img.shields.io/badge/bahasa%20UI-6-e0870b)

</div>

> [!WARNING]
> **Peringatan hukum & keselamatan baca sebelum memakai.**
> Ereshkigal adalah alat **uji keamanan** Wi-Fi. Gunakan **hanya**:
> - pada jaringan dan perangkat **milik Anda sendiri**, atau yang Anda miliki **izin tertulis** untuk diuji;
> - di dalam **lingkungan lab / percobaan terkendali** yang Anda siapkan untuk pengujian.
>
> **Jangan** memakainya terhadap jaringan, perangkat, atau orang yang tidak Anda
> berwenang menguji. Menyadap atau mengganggu jaringan nirkabel tanpa izin adalah
> **ilegal di sebagian besar negara** dan dapat berujung pada **tuntutan pidana**.
> Proyek ini hanya untuk edukasi, riset, CTF, dan uji penetrasi resmi. **Anda
> sendiri yang bertanggung jawab atas penggunaannya.**

---

<p align="center">
  <img src="assets/screenshot-flasher.png" width="330" alt="Ereshkigal Project (Windows)">
  &nbsp;&nbsp;
  <img src="assets/screenshot-device.png" width="300" alt="Web UI perangkat Ereshkigal">
</p>
<p align="center"><sub>Kiri: flasher di Windows. Kanan: dasbor web bawaan perangkat setelah di-flash.</sub></p>

## Isi folder

| Berkas | Keterangan |
|--------|------------|
| **`EreshkigalFlasher.exe`** | Aplikasi flashing (Windows, mandiri). |
| **`Ereshkigal.efw`** | Firmware, dalam format terlindungi Ereshkigal. |

Distribusikan kedua berkas bersamaan. Aplikasinya jendela native kecil dalam
**English, Bahasa Indonesia, Español, Français, Deutsch, dan 中文** ganti dari
pemilih di kanan atas.

## Kebutuhan

- **Windows 10 atau 11.** Memakai **WebView2 runtime** bawaan (sudah ada di
  Windows 11 dan Windows 10 terkini; jika belum, pasang *Microsoft Edge WebView2
  Runtime* gratis sekali saja).
- Papan **RTL8720DN / BW16** dan kabel USB **data**.
- **Driver USB-serial** papan (umumnya CH340 atau CP2102) agar muncul sebagai
  port `COM`.

## Tutorial flash dalam 4 langkah

1. **Colok** papan ke USB lalu jalankan **`EreshkigalFlasher.exe`**.
2. `Ereshkigal.efw` sudah terpilih otomatis. Pilih **port COM** papan dari daftar
   (tekan tombol muat ulang jika belum ada cabut/colok lagi papan lalu muat
   ulang; entri yang muncul itulah papan Anda).
3. Biarkan **Kecepatan** di `1500000`.
4. Klik **Flash firmware**, tunggu **Selesai**, lalu matikan-nyalakan papan.

Kebanyakan papan masuk mode flashing sendiri. **Jika log macet**, lakukan urutan
tombol **Mode download** pada papan:

```
   ┌── 1 ──┐      ┌── 2 ──┐      ┌── 3 ──┐
   │ BOOT  │  →   │ RESET │  →   │ BOOT  │
   │ tahan │      │ tekan │      │ lepas │
   └───────┘      └───────┘      └───────┘
   tahan BOOT  ·  tekan RESET  ·  lepas BOOT
```

Flasher mengulang sinkronisasi otomatis (hingga 3×).

## Boot pertama setelah flash

1. Perangkat memancarkan Wi-Fi **terbuka** bernama **`Ereshkigal`**.
2. Sambungkan, buka **http://192.168.1.1/**.
3. Selesaikan **wizard setup** sekali atur nama jaringan dan kata sandi (8–63
   karakter). Perangkat menyimpannya dan reboot.
4. Sambung ulang dengan kata sandi Anda, buka lagi **http://192.168.1.1/**, dan
   dasbor lengkap terbuka.

## Memakainya untuk uji keamanan WPA2 → WPA3

Ereshkigal memperlihatkan kelemahan Wi-Fi yang nyata dan umum: jaringan **WPA2
tanpa Protected Management Frames (PMF / 802.11w)** bisa diganggu dengan frame
**deauthentication** palsu  siapa pun di sekitar dapat memutus klien, dan
pemutusan paksa itu adalah langkah awal di balik penangkapan handshake dan
serangan evil-twin.

Alur pengujian **resmi** pada jaringan milik Anda sendiri:

1. **Scan**  buka dasbor, tekan *Scan*, pilih jaringan target Anda.
2. **Users**  lihat perangkat yang sedang terhubung.
3. **Attack**  jalankan uji *deauth* dan amati klien Anda sendiri.
4. **Detector**  dedikasikan radio untuk mendeteksi frame deauth di udara.

**Membaca hasil**
- Klien **terputus** → jaringan WPA/WPA2 tanpa PMF wajib dan rentan terhadap
  pemalsuan management frame (deauth denial-of-service, lalu rantai
  putus-lalu-tangkap yang menyusul).
- Klien **tetap terhubung** → management frame sudah terlindungi.

**Solusinya  beralih ke WPA3.** Ubah jaringan ke **WPA3 (SAE)**, atau minimal
**WPA2 dengan PMF disetel _required_** (802.11w). WPA3 mewajibkan management frame
terlindungi, sehingga deauth/disassociation palsu diabaikan. **Jalankan ulang uji
deauth yang sama**  klien seharusnya tetap terhubung, membuktikan peningkatan itu
menutup celah. Perbandingan sebelum/sesudah itulah intinya: pakai Ereshkigal untuk
membenarkan dan memverifikasi migrasi WPA2 → WPA3.

> Hanya pada jaringan milik Anda atau yang Anda berwenang menguji, di lab terkendali.

## Pemecahan masalah

| Gejala | Solusi |
|--------|--------|
| **Tidak ada port COM** | Pasang driver USB-serial; pakai kabel data (bukan hanya cas). |
| **"Failed to open COM…"** | Port dipakai program lain (serial monitor, flasher lain). Tutup dulu. |
| **Mengulang terus lalu gagal** | Lakukan urutan Mode download saat mengulang: tahan BOOT, tekan RESET, lepas BOOT. |
| **Masih gagal** | Turunkan **Kecepatan** ke `921600` lalu flash lagi. |

## Tentang format firmware

`Ereshkigal.efw` adalah firmware dalam format paket milik Ereshkigal. Flasher
menyiapkannya untuk papan secara internal Anda tak perlu membongkar apa pun dan
tak butuh alat tambahan. Simpan `.exe` dan `.efw` bersama.

---

<div align="center">
<sub>Ereshkigal oleh <b>Titan Digitalsoft</b> · Flasher 2.0.0 · Hanya untuk pengujian resmi</sub>
</div>
