# Laporan Praktikum 5: Job Control & Shell Management
**Mata Kuliah:** Sistem Operasi  
**Fakultas:** Ilmu Komputer, Universitas Sriwijaya  

---

## 📋 Daftar Isi

1. [Persiapan Awal & Lingkungan Kerja](#1-persiapan-awal--lingkungan-kerja)
2. [Percobaan 1: Profile](#2-percobaan-1-profile)
3. [Percobaan 2: History](#3-percobaan-2-history)
4. [Percobaan 3: Membuat Bash-script dan Menjalankannya](#4-percobaan-3-membuat-bash-script-dan-menjalankannya)
5. [Percobaan 4: Job Control](#5-percobaan-4-job-control)
6. [Percobaan 5: Manipulasi Stack untuk Direktori](#6-percobaan-5-manipulasi-stack-untuk-direktori)
7. [Percobaan 6: Alias](#7-percobaan-6-alias)
8. [Penyelesaian Tugas & Contoh Output (Exercises & Tasks)](#8-penyelesaian-tugas--contoh-output-exercises--tasks)

---

## 1. Persiapan Awal & Lingkungan Kerja

Masuk ke sistem operasi Linux menggunakan kredensial standar praktikum:
* **Username**: `mahasiswa`
* **Password**: `mahasiswa`

---

## 2. Percobaan 1: Profile

Melihat dan memahami konfigurasi file profile dan environment pengguna.

### Perintah:
```bash
# Melihat seluruh file (termasuk hidden file) di home direktori
ls -la

# Melihat isi file .bash_profile
more ~/.bash_profile

# Melihat file .bash_logout
cat ~/.bash_logout
```

### Contoh Output:
```text
mahasiswa@ubuntu:~$ ls -la
total 36
drwxr-xr-x 5 mahasiswa mahasiswa 4096 Oct 13 08:00 .
drwxr-xr-x 3 root      root      4096 Oct 13 07:50 ..
-rw-r--r-- 1 mahasiswa mahasiswa  220 Oct 13 07:50 .bash_logout
-rw-r--r-- 1 mahasiswa mahasiswa 3526 Oct 13 07:50 .bashrc
-rw-r--r-- 1 mahasiswa mahasiswa  675 Oct 13 07:50 .profile

mahasiswa@ubuntu:~$ cat ~/.bash_logout
# ~/.bash_logout: executed by bash(1) when login shell exits.
clear
```

---

## 3. Percobaan 2: History

Mengelola catatan instruksi perintah terminal.

### Perintah:
```bash
# Mengecek batasan maksimum ukuran history (HISTSIZE)
echo $HISTSIZE

# Menampilkan seluruh riwayat instruksi beserta nomor urutnya
history

# Menggunakan perintah fix command (fc) untuk melihat history
fc -l 1 5
```

### Contoh Output:
```text
mahasiswa@ubuntu:~$ echo $HISTSIZE
1000

mahasiswa@ubuntu:~$ fc -l 1 5
    1  ls -la
    2  more ~/.bash_profile
    3  cat ~/.bash_logout
    4  echo $HISTSIZE
    5  history
```

---

## 4. Percobaan 3: Membuat Bash-script dan Menjalankannya

Membuat dan mengeksekusi skrip shell dasar.

### Perintah & Langkah:
1. Buat file `pl.sh`:
   ```bash
   nano pl.sh
   ```
   Isi file:
   ```bash
   #!/bin/bash
   echo "Program bash script"
   echo "Nama Mahasiswa: Fauzan Aulia"
   echo "Sistem Komputer"
   ```

2. Ubah hak akses menjadi executable dan jalankan:
   ```bash
   chmod +x pl.sh
   ./pl.sh
   ```

### Contoh Output:
```text
mahasiswa@ubuntu:~$ ./pl.sh
Program bash script
Nama Mahasiswa: Fauzan Aulia
Sistem Komputer
```

---

## 5. Percobaan 4: Job Control

Mengelola proses foreground dan background.

### Perintah:
```bash
# Menjalankan loop di background menggunakan &
./ploop.sh &

# Memeriksa job yang aktif
jobs
```

### Contoh Output:
```text
mahasiswa@ubuntu:~$ ./ploop.sh &
[1] 4125
mahasiswa@ubuntu:~$ jobs
[1]+  Running                 ./ploop.sh &
```

---

## 6. Percobaan 5: Manipulasi stack untuk Direktori

Navigasi direktori menggunakan stack (`dirs`, `pushd`, `popd`).

### Perintah:
```bash
mkdir marketing sales support
pushd sales
pwd
dirs
```

### Contoh Output:
```text
mahasiswa@ubuntu:~/sales$ pwd
/home/mahasiswa/sales
mahasiswa@ubuntu:~/sales$ dirs
~/sales ~
```

---

## 7. Percobaan 6: Alias

Membuat shortcut untuk perintah terminal.

### Perintah:
```bash
alias del='rm -i'
alias h='history'
h | head -n 3
```

### Contoh Output:
```text
mahasiswa@ubuntu:~$ h | head -n 3
    1  ls -la
    2  echo $HISTSIZE
    3  alias
```

---

## 8. Penyelesaian Tugas & Contoh Output (Exercises & Tasks)

### 1. Eksekusi Seluruh Profile & `su` vs `su -`

* **Perbedaan `su mahasiswa` dan `su - mahasiswa`**:
  * `su mahasiswa`: Mengganti user aktif ke `mahasiswa`, namun **tetap mempertahankan variabel lingkungan (environment PATH)** dari user sebelumnya. File profile (`.bash_profile`, dll) **tidak** dimuat ulang.
  * `su - mahasiswa`: Mengganti user dengan **membersihkan environment lama dan memuat ulang full login shell** dari awal, termasuk mengeksekusi `/etc/profile` dan konfigurasi profile home direktori user baru.

---

### 2. Prompt String (PS1) Eksperimen

### Perintah:
```bash
PS1='> '
export PS1
# Setelah prompt berubah menjadi '>'
PS1='\t> '
```

### Contoh Output:
```text
> PS1='\t> '
10:10:20> pwd
/home/mahasiswa
10:10:25> 
```

---

### 3. Logout Script (`.bash_logout`)

### Perintah & Konfigurasi:
Edit file `~/.bash_logout`:
```bash
nano ~/.bash_logout
```
Isi file:
```bash
echo "Terima kasih atas sesi yang diberikan"
sleep 5
clear
```

### Contoh Output saat Logout (`exit`):
```text
mahasiswa@ubuntu:~$ exit
Terima kasih atas sesi yang diberikan
[Sistem akan jeda selama 5 detik, lalu membersihkan layar sebelum menutup terminal/sesi]
```

---

### 4. Bash Script Tugas (`p1.sh`, `p2.sh`, `p3.sh`)

### Perintah Eksekusi Sesuai Tugas:
```bash
# Menjalankan berurutan dengan separator titik koma (;)
./p1.sh; ./p3.sh; ./p2.sh
```

### Contoh Output:
```text
mahasiswa@ubuntu:~$ ./p1.sh; ./p3.sh; ./p2.sh
Program p1
total 16
-rwxr-xr-x 1 mahasiswa mahasiswa 35 Oct 13 08:15 p1.sh
-rwxr-xr-x 1 mahasiswa mahasiswa 35 Oct 13 08:15 p2.sh
Program p3
  PID TTY          TIME CMD
 2840 pts/0    00:00:00 bash
 4201 pts/0    00:00:00 ps
Program p2
mahasiswa pts/0        2026-10-13 07:50 (:0)
```

---

### 5. Jobs & Process Management (`pwaktu.sh`)

### Perintah & Eksekusi:
```bash
# Jalankan skrip pencatat waktu di background
./pwaktu.sh &

# Jalankan utilitas find ke background dan alihkan error ke /dev/null
find / -print > files 2>/dev/null &

# Periksa status jobs
jobs
```

### Contoh Output:
```text
mahasiswa@ubuntu:~$ ./pwaktu.sh &
[1] 4512
mahasiswa@ubuntu:~$ find / -print > files 2>/dev/null &
[2] 4513
mahasiswa@ubuntu:~$ jobs
[1]   Running                 ./pwaktu.sh &
[2]-  Running                 find / -print > files 2>/dev/null &
```

---

### 6. History Tasks

### Perintah:
```bash
# Ganti nilai HISTSIZE menjadi 20
HISTSIZE=20

# Mengulang instruksi terakhir
!!

# Mengulangi instruksi dengan prefix tertentu
!ls
```

### Contoh Output:
```text
mahasiswa@ubuntu:~$ HISTSIZE=20
mahasiswa@ubuntu:~$ !!
HISTSIZE=20
mahasiswa@ubuntu:~$ !ls
ls -la
total 24
drwxr-xr-x 3 mahasiswa mahasiswa 4096 Oct 13 08:30 .
drwxr-xr-x 3 root      root      4096 Oct 13 07:50 ..
-rwxr-xr-x 1 mahasiswa mahasiswa   42 Oct 13 08:15 p1.sh
```

*Dokumentasi lengkap ini disusun untuk mempermudah pemahaman praktikum Sistem Operasi Universitas Sriwijaya.*
