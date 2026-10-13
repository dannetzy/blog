---
layout: post
title: "Perintah Dasar Linux yang Wajib Dikuasai"
subtitle: "Panduan navigasi CLI untuk pemula dan anak jaringan"
tags: [linux, terminal, cli, debian]
---

Dalam dunia Teknik Komputer dan Jaringan, menguasai sistem operasi Linux adalah sebuah keharusan. Entah itu saat mengkonfigurasi server berbasis Debian, menjalankan *environment* pengembangan web di WSL (Windows Subsystem for Linux), atau bahkan ngoprek server *voip* lokal menggunakan Termux di Android, semuanya bermuara pada satu hal: *Command Line Interface* (CLI).

Bagi yang baru beralih dari antarmuka grafis (GUI) ke layar terminal hitam, CLI mungkin terlihat mengintimidasi. Namun, dengan menguasai beberapa perintah dasar berikut, navigasi dan manajemen sistem akan terasa jauh lebih efisien.

### 1. `pwd` (Print Working Directory)
Saat pertama kali membuka terminal, terkadang kita tidak yakin sedang berada di folder mana. Perintah ini akan mencetak *path* atau jalur lengkap direktori tempat kita berada saat ini.

```bash
pwd
# Contoh Output: /home/username/blog

```

### 2. `ls` (List)

Digunakan untuk melihat isi dari sebuah direktori.

```bash
ls          # Menampilkan file dan folder biasa
ls -l       # Menampilkan detail (hak akses, ukuran, pemilik)
ls -a       # Menampilkan semua file, termasuk file tersembunyi (hidden files)

```

### 3. `cd` (Change Directory)

Ini adalah perintah untuk berpindah-pindah folder.

```bash
cd /var/www/html  # Pindah ke direktori spesifik
cd ..             # Mundur satu folder ke belakang
cd ~              # Langsung kembali ke direktori /home user

```

### 4. `mkdir` & `touch` (Membuat Folder & File)

Daripada repot klik kanan lalu "New Folder", kamu bisa langsung membuatnya dari terminal.

```bash
mkdir nama_folder  # Membuat folder baru
touch index.html   # Membuat file kosong baru bernama index.html

```

### 5. `cp` & `mv` (Copy & Move)

Perintah untuk menyalin atau memindahkan file. `mv` juga sering digunakan untuk mengubah nama (*rename*) file.

```bash
cp file1.txt file2.txt        # Menyalin file1.txt menjadi file2.txt
cp -r folder1 folder2         # Menyalin seluruh folder dan isinya
mv gambar.jpg /home/Pictures/ # Memindahkan gambar ke folder Pictures
mv lama.txt baru.txt          # Mengubah nama file

```

### 6. `rm` (Remove)

Hati-hati dengan perintah ini karena file yang dihapus melalui terminal tidak masuk ke *Recycle Bin*.

```bash
rm file.txt       # Menghapus file
rm -r folder_lama # Menghapus folder beserta seluruh isinya

```

### 7. `sudo` (Superuser Do)

Dalam Linux (terutama keluarga Ubuntu/Debian), user biasa dibatasi hak aksesnya demi keamanan. Jika kamu perlu menginstal aplikasi atau mengubah konfigurasi sistem jaringan, tambahkan `sudo` di depannya agar dieksekusi sebagai *Administrator* (root).

```bash
sudo apt update
sudo nano /etc/network/interfaces

```

---

**Tips:** Di Linux, terminal sangat sensitif terhadap huruf besar dan kecil (*case-sensitive*). File `Index.html` dan `index.html` dianggap sebagai dua file yang berbeda. Jangan ragu untuk sering menggunakan tombol **Tab** di *keyboard* untuk melengkapi nama file secara otomatis (*auto-complete*).