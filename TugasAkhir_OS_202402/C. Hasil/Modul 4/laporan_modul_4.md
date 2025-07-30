# 📝 Laporan Tugas Akhir

* Mata Kuliah: Sistem Operasi
* Semester: Genap / Tahun Ajaran 2024–2025
**Nama**: Novi Fitriyani
**NIM**: 240202843
**Modul yang Dikerjakan**: Modul 4 – Subsistem Kernel Alternatif (xv6-public)

---

## 📌 Deskripsi Singkat Tugas

Modul 4 – Subsistem Kernel Alternatif:
Menambahkan dua fitur ke sistem operasi xv6, yaitu:
- chmod(path, mode) syscall untuk mengatur mode file (read-only atau read-write)
- Driver pseudo-device /dev/random yang menghasilkan byte acak saat dibaca
---

## 🛠️ Rincian Implementasi

* Menambahkan sistem call chmod:
  - Menambahkan fungsi sys_chmod pada sysfile.c
  - Menambahkan nomor syscall baru pada syscall.h, dan deklarasinya di user.h, usys.S
  - Menambahkan field baru mode di struct inode pada fs.h
  - Memodifikasi fungsi writei() untuk mengecek flag read-only sebelum menulis
* Menambahkan device /dev/random:
  - Menambahkan entry major device baru di ide.c atau sysfile.c
  - Implementasi fungsi randomread() yang menghasilkan byte pseudo-random
  - Register device dengan mknod("/dev/random", 1, 3); di init.c
* Menambahkan program uji:
  - chmodtest.c untuk menguji apakah file read-only tidak bisa ditulis
  - randomtest.c untuk membaca 8 byte dari /dev/random dan mencetaknya

---

## ✅ Uji Fungsionalitas

* chmodtest: untuk menguji syscall chmod(path, mode)
* randomtest: untuk menguji pembacaan dari /dev/random

---

## 📷 Hasil Uji

Lampirkan hasil uji berupa screenshot atau output terminal.

### 📍 Output `chmodtest`:

```
Write blocked as expected
```

### 📍 Output `randomtest`:

```
20 51 41 143 164 3 115 56
```

📷 Screenshot:

```
![hasil cowtest](./screenshots/cowtest_output.png)
```

---

## ⚠️ Kendala yang Dihadapi

* File /dev/random tidak otomatis muncul setelah booting ulang — solusinya dengan menambahkan perintah mknod ke init.c
* Kesalahan pada register device major menyebabkan panic saat akses device
* Permasalahan read-only baru terdeteksi setelah writei() dimodifikasi

---

## 📚 Referensi

* Buku xv6 MIT: https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf
* Repositori xv6-public: https://github.com/mit-pdos/xv6-public
* Diskusi praktikum dan eksperimen langsung dengan xv6

---
