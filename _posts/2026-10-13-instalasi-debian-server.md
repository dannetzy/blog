---
layout: post
title: "Panduan Instalasi Debian Server untuk Pemula"
subtitle: "Langkah-langkah membangun server Linux dari nol menggunakan Debian"
tags: [linux, debian, server, sysadmin]
---

Sebagai anak Teknik Komputer dan Jaringan, membangun server sendiri adalah keterampilan dasar yang wajib dikuasai. Debian sering menjadi pilihan utama untuk *server* karena stabilitasnya yang luar biasa, sifatnya yang *open-source*, dan fakta bahwa ia adalah induk dari distribusi populer lainnya seperti Ubuntu.

Dalam panduan ini, kita akan membahas instalasi **Debian Server (Mode CLI / Tanpa GUI)**, yang merupakan standar industri untuk menghemat *resource* (RAM dan CPU).

### Persiapan Instalasi

Sebelum mulai, pastikan kamu sudah menyiapkan:
1. **File ISO Debian:** Unduh versi *Netinst* (Network Installer) terbaru dari situs resmi Debian. File ini ukurannya kecil karena paket tambahan akan diunduh lewat internet saat instalasi.
2. **Media Instalasi:** *Flashdisk* yang sudah dibuat *bootable* (bisa menggunakan Rufus atau BalenaEtcher), atau *Virtual Machine* (VM) seperti VirtualBox / VMware jika kamu hanya ingin berlatih.
3. **Koneksi Internet:** Karena kita menggunakan versi *Netinst*, pastikan mesin terhubung ke internet (menggunakan kabel LAN lebih disarankan).

---

### Langkah-langkah Instalasi

#### 1. Booting dan Pemilihan Mode
Nyalakan PC/Server atau jalankan VM, lalu *boot* melalui ISO Debian. Pada layar pertama (GRUB menu), pilih **Install** (bukan *Graphical Install*, karena kita akan membiasakan diri dengan antarmuka teks).

#### 2. Bahasa, Lokasi, dan Keyboard
*   **Language:** Pilih *English* (disarankan agar lebih mudah *troubleshooting* jika terjadi *error*).
*   **Location:** Pilih *Other* -> *Asia* -> *Indonesia*.
*   **Locales:** Pilih *United States - en_US.UTF-8*.
*   **Keymap:** Pilih *American English* (standar *keyboard* QWERTY).

#### 3. Konfigurasi Jaringan (Network)
Sistem akan mencoba mendapatkan IP otomatis via DHCP.
*   **Hostname:** Beri nama untuk server kamu, misalnya `srv-danne`.
*   **Domain Name:** Jika kamu punya domain lokal, isi di sini (contoh: `lab.local`). Jika tidak, kosongkan saja.

#### 4. Setup User dan Password (PENTING!)
Debian memisahkan akses *Superuser* (root) dengan *User* biasa.
*   **Root Password:** Masukkan *password* yang kuat untuk akun *Administrator* (root). Jangan sampai lupa!
*   **Full Name for the new user:** Masukkan nama lengkap kamu (misal: `M. Danne Febrian`).
*   **Username for your account:** Masukkan *username* untuk *login* sehari-hari (misal: `danne`).
*   **User Password:** Masukkan *password* untuk akun biasa ini.

#### 5. Partisi Harddisk
Untuk pemula, pilih opsi otomatis. Jika kamu sudah paham struktur Linux, kamu bisa memilih *Manual*.
*   Pilih **Guided - use entire disk**.
*   Pilih harddisk yang akan diinstal.
*   Pilih **All files in one partition (recommended for new users)**.
*   Pilih **Finish partitioning and write changes to disk**, lalu pilih **Yes**.

#### 6. Konfigurasi Package Manager (APT)
*   **Scan extra installation media?** Pilih *No*.
*   **Debian archive mirror country:** Pilih *Indonesia* agar proses unduhan paket (*update/install* aplikasi nantinya) lebih cepat karena menggunakan server lokal (seperti Kartolo atau server kampus).
*   **Debian archive mirror:** Pilih salah satu (misal: `kebo.pens.ac.id` atau `kartolo.sby.datautama.net.id`).
*   **HTTP proxy:** Kosongkan jika kamu tidak menggunakan *proxy*.

#### 7. Pemilihan Software (Software Selection)
Ini adalah tahap paling krusial untuk server.
*   *Participate in the package usage survey?* Pilih *No*.
*   Pada daftar *software*, **HILANGKAN TANDA BINTANG (*)** pada opsi `Debian desktop environment` dan `GNOME` (Gunakan tombol Spasi untuk menghilangkan/memberi tanda bintang).
*   **PASTIKAN TANDA BINTANG (*)** hanya ada pada:
    *   `SSH server` (Wajib, agar server bisa diremote menggunakan PuTTY atau terminal).
    *   `Standard system utilities`.

#### 8. Instalasi GRUB Boot Loader
*   *Install the GRUB boot loader to your primary drive?* Pilih **Yes**.
*   Pilih *harddisk* utama kamu (biasanya `/dev/sda` atau `/dev/vda`).

#### 9. Selesai!
Pilih **Continue** untuk me-*reboot* sistem. Jangan lupa cabut *flashdisk* / *unmount* ISO agar tidak masuk ke menu instalasi lagi.

---

### Langkah Pertama Setelah Instalasi

Setelah *reboot*, kamu akan disambut layar hitam bertuliskan `srv-danne login:`. 
Masuk menggunakan *username* dan *password* biasa yang kamu buat di langkah 4.

Setelah masuk, cobalah mengecek alamat IP server kamu agar bisa diremote melalui SSH dari laptop utama:

```bash
ip a```