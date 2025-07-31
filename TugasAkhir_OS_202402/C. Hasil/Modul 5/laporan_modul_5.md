# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi  
**Semester**: Genap / Tahun Ajaran 2024–2025  
**Nama**: Novi Fitriyani  
**NIM**: 240202843  
**Modul yang Dikerjakan**: Modul 5 – Audit dan Keamanan Sistem (xv6-public)  

---

## 📌 Deskripsi Singkat Tugas

Modul 5 – Audit dan Keamanan Sistem (xv6-public):
- Mengimplementasikan fitur audit logging untuk semua system call yang dipanggil oleh proses, serta menambahkan syscall get_audit_log() agar log bisa diakses dari ruang pengguna (user space). Audit berguna untuk mencatat aktivitas sistem secara ringkas untuk keperluan debugging dan keamanan.
---

## 🛠️ Rincian Implementasi

* Menambahkan struktur struct audit_entry untuk menyimpan log setiap syscall (audit.h)
* Membuat array global audit_log[MAX_AUDIT] di audit.c sebagai buffer log melingkar
* Menyisipkan logging ke semua entri syscall di syscall() (dalam trap.c)
* Menambahkan syscall baru get_audit_log() di sysproc.c, usys.S, syscall.c, dan syscall.h
* Syscall get_audit_log() hanya dapat dipanggil oleh proses tertentu (misal PID 1 atau audit user program)
* Membuat program pengguna audit.c untuk menampilkan isi log ke terminal

---

## ✅ Uji Fungsionalitas

* audit: Untuk mencetak semua log syscall yang telah terekam oleh kernel, termasuk informasi PID, nomor SYSCALL, dan TICK saat syscall terjadi.

---

## 📷 Hasil Uji

Lampirkan hasil uji berupa screenshot atau output terminal.

### 📍 Output audit (dijalankan oleh PID 1):

```
=== Audit Log ===
[0] PID=1 SYSCALL=7 TICK=12
[1] PID=1 SYSCALL=15 TICK=14
[2] PID=1 SYSCALL=17 TICK=20
[3] PID=1 SYSCALL=15 TICK=21
[4] PID=1 SYSCALL=10 TICK=21
[5] PID=1 SYSCALL=10 TICK=21
[6] PID=1 SYSCALL=16 TICK=22
[7] PID=1 SYSCALL=16 TICK=22
[8] PID=1 SYSCALL=16 TICK=22
[9] PID=1 SYSCALL=16 TICK=22
[10] PID=1 SYSCALL=16 TICK=22
[11] PID=1 SYSCALL=16 TICK=22
[12] PID=1 SYSCALL=16 TICK=23
[13] PID=1 SYSCALL=16 TICK=23
[14] PID=1 SYSCALL=16 TICK=23
[15] PID=1 SYSCALL=16 TICK=23
[16] PID=1 SYSCALL=16 TICK=23
[17] PID=1 SYSCALL=16 TICK=23
[18] PID=1 SYSCALL=16 TICK=23
[19] PID=1 SYSCALL=16 TICK=25
[20] PID=1 SYSCALL=16 TICK=25
[21] PID=1 SYSCALL=16 TICK=25
[22] PID=1 SYSCALL=16 TICK=25
[23] PID=1 SYSCALL=16 TICK=25
[24] PID=1 SYSCALL=1 TICK=26
[25] PID=2 SYSCALL=7 TICK=32
[26] PID=2 SYSCALL=15 TICK=33
[27] PID=2 SYSCALL=21 TICK=33
[28] PID=2 SYSCALL=16 TICK=34
[29] PID=2 SYSCALL=16 TICK=34
[30] PID=2 SYSCALL=5 TICK=6584
[31] PID=2 SYSCALL=5 TICK=6584
[32] PID=2 SYSCALL=5 TICK=6584
[33] PID=2 SYSCALL=5 TICK=6584
[34] PID=2 SYSCALL=5 TICK=6584
[35] PID=2 SYSCALL=5 TICK=6584
[36] PID=2 SYSCALL=1 TICK=6585
[37] PID=3 SYSCALL=12 TICK=6585
[38] PID=3 SYSCALL=7 TICK=6588
```

### 📍 Output audit (dijalankan oleh PID 1):

```
Access denied or error
```

📷 Screenshot:

<img width="701" height="984" alt="image" src="https://github.com/user-attachments/assets/e290b9fd-dab4-4e85-a69f-eaedc2b626d1" />

<img width="943" height="463" alt="image" src="https://github.com/user-attachments/assets/f2b7d58b-cb89-4724-9e17-2a9f259a7426" />


```
```
---

## ⚠️ Kendala yang Dihadapi

* Awalnya validasi syscall get_audit_log() hanya mengizinkan PID 1 (init) untuk mengakses log. Hal ini membatasi pengujian, sehingga validasi akses sementara di-nonaktifkan agar program audit dapat berjalan.
* Penggunaan argptr() perlu disesuaikan dengan benar untuk menghindari page fault saat memmove() dipanggil dari kernel.

---

## 📚 Referensi

* Buku xv6 MIT: https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf
* Repositori xv6-public: https://github.com/mit-pdos/xv6-public
* Diskusi praktikum dan debugging bersama asisten
* Dokumentasi syscall dan memory di xv6

---
