---
layout: post
title: "Keamanan Jaringan 101: Langkah Pertama Mengamankan Server"
subtitle: "Praktik dasar cyber security untuk SysAdmin dan Network Engineer"
tags: [cybersecurity, linux, jaringan, server, mikrotik]
---

Setelah berhasil melakukan instalasi sistem operasi pada server (seperti Debian atau Ubuntu) atau mengkonfigurasi *router* ke jaringan publik, pekerjaan kita sebenarnya belum selesai. Ancaman *cyber security* seperti serangan *brute-force*, pemindaian *port* otomatis (*port scanning*), hingga eksploitasi celah keamanan mengintai setiap detik.

Dalam dunia Teknik Komputer dan Jaringan, *hardening* (memperkuat keamanan sistem) adalah kewajiban. Berikut adalah langkah-langkah esensial untuk mengamankan server dan infrastruktur jaringan kamu dari serangan dasar.

### 1. Terapkan *Principle of Least Privilege*
Jangan pernah menggunakan akun `root` (Superuser) untuk aktivitas operasional sehari-hari. Akun `root` memiliki kekuasaan tak terbatas; jika terjadi kesalahan perintah atau akun ini diretas, seluruh sistem akan hancur.
*   **Praktik Baik:** Selalu gunakan akun *user* biasa. Jika membutuhkan hak akses administratif, gunakan perintah `sudo`. 

### 2. Amankan Akses Remote (SSH & WinBox)
Layanan *remote* seperti SSH (Port 22) dan MikroTik WinBox (Port 8291) adalah target paling sering diserang oleh *bot* dari seluruh dunia.
*   **Disable Root Login SSH:** Edit konfigurasi SSH (`/etc/ssh/sshd_config`) dan ubah `PermitRootLogin` menjadi `no`.
*   **Ganti Port Default:** Ubah *port default* SSH ke *port* acak (misal: 2222) untuk menghindari skrip *bot* otomatis.
*   **Gunakan SSH Keys:** Tinggalkan *password* konvensional dan beralih ke otentikasi menggunakan *Public/Private Key* (*RSA* atau *Ed25519*). Ini jauh lebih tahan terhadap serangan *brute-force*.

### 3. Konfigurasi Firewall dengan Ketat
*Firewall* adalah satpam yang menjaga pintu masuk dan keluar jaringan kamu.
*   **Di Linux Server:** Gunakan **UFW (Uncomplicated Firewall)** atau **Iptables**. Konfigurasi aturan dasar: *Deny all incoming, allow all outgoing*. Setelah itu, buka hanya *port* yang benar-benar dibutuhkan (misalnya *port* 80/443 untuk Web, dan *port* SSH kustom).
*   **Di MikroTik:** Manfaatkan fitur **IP -> Firewall -> Filter Rules**. Blokir akses DNS dari luar (*drop input* pada *port* 53 di *interface* publik) agar *router* tidak dijadikan alat serangan *DDoS Amplification*. Kamu juga bisa mengonfigurasi *Layer 7 Protocols* untuk memblokir trafik spesifik.

### 4. Tutup Layanan yang Tidak Digunakan
Semakin banyak aplikasi dan *port* yang terbuka, semakin luas "permukaan serangan" (*attack surface*). Jika server kamu didedikasikan hanya untuk web server dan database lokal, pastikan layanan lain (seperti FTP atau VoIP Asterisk yang tidak dipakai) dimatikan atau bahkan di-*uninstall*.
Gunakan perintah ini untuk mengecek *port* apa saja yang sedang mendengarkan (*listening*) di server Linux:
```bash
sudo ss -tulpn

```

### 5. Selalu Update & Patch Sistem

Banyak peretasan terjadi bukan karena *hacker* yang sangat jenius, melainkan karena SysAdmin yang malas melakukan *update*. Celah keamanan (*bug*) baru ditemukan hampir setiap hari.
Lakukan pembaruan secara berkala:

```bash
sudo apt update && sudo apt upgrade -y

```

### Kesimpulan

*Cyber security* bukanlah sesuatu yang disetel sekali lalu ditinggalkan. Ini adalah proses berkelanjutan untuk terus memonitor, menambal celah, dan menganalisis *log* (catatan aktivitas) jaringan. Dengan menerapkan kelima langkah di atas, kamu sudah menyingkirkan 90% ancaman dasar yang mengincar server publik.
