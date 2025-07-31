# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi  
**Semester**: Genap / Tahun Ajaran 2024–2025  
**Nama**: Novi Fitriyani  
**NIM**: 240202843  
**Modul yang Dikerjakan**: Modul 1 – System Call dan Instrumentasi Kernel  

---

## 📌 Deskripsi Singkat Tugas
Modul 1 – System Call dan Instrumentasi Kernel:
- getpinfo() untuk menampilkan daftar proses aktif beserta PID, penggunaan memori, dan nama proses.
- getReadCount() untuk menghitung jumlah pemanggilan fungsi read() sejak sistem dinyalakan.

---

## 🛠️ Rincian Implementasi

- Menambahkan system call sys_getpinfo() dan sys_getreadcount() di file sysproc.c.
- Mendaftarkan syscall baru pada: syscall.c, syscall.h, usys.S, dan user.h
- Menambahkan struktur struct pinfo di proc.h untuk menyimpan data proses.
- Menambahkan variabel global readcount di kernel untuk mencatat jumlah pemanggilan read().
- Membuat dua program uji: ptest.c dan rtest.c

---

## ✅ Uji Fungsionalitas
Program uji yang digunakan:
- ptest: menampilkan informasi tiga proses yang sedang aktif (init, sh, ptest)
- rtest: menampilkan nilai readcount sebelum dan sesudah melakukan pembacaan (misalnya input string “hello”)

---

## 📷 Hasil Uji

Lampirkan hasil uji berupa screenshot atau output terminal.

### 📍 Output `ptest`:

```
PID     MEM     NAME
1       12288   init
2       16384   sh
3       12288   ptest
```

### 📍 Contoh Output `rtest`:

```
Read Count Sebelum: 12
hello
Read Count Setelah: 13
```
---

📸 Screenshot:

<img width="940" height="514" alt="image" src="https://github.com/user-attachments/assets/0ed8e068-229e-4eec-9063-8a5ab235ec24" />



---

## ⚠️ Kendala yang Dihadapi

- Awalnya terjadi error karena kesalahan pemanggilan pointer terhadap ptable yang merupakan pointer ke struktur struct pinfo, bukan struct proc.
- Juga terjadi error incomplete type karena belum meng-include header yang berisi definisi spinlock (#include "spinlock.h").
- Perlu perhatian khusus dalam penggunaan argptr() dan struktur pointer untuk syscall agar data tidak corrupt.

---

## 📚 Referensi

- Buku xv6 MIT: https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf
- Repositori xv6-public: https://github.com/mit-pdos/xv6-public
- Forum diskusi dan dokumentasi praktikum

---
