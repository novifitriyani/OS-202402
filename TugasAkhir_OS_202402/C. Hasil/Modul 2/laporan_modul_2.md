# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: Novi Fitriyani
**NIM**: 240202843
**Modul yang Dikerjakan**: Modul 2 — Penjadwalan CPU Lanjutan (Priority Scheduling Non-Preemptive)

---

## 📌 Deskripsi Singkat Tugas
Modul 2 – Penjadwalan CPU Lanjutan:
- Mengubah algoritma penjadwalan default (Round Robin) menjadi algoritma Non-Preemptive Priority Scheduling pada sistem operasi xv6. Proses dengan prioritas lebih tinggi (angka prioritas lebih kecil) akan dipilih untuk dijalankan terlebih dahulu tanpa interupsi hingga proses selesai atau berubah status.
---

## 🛠️ Rincian Implementasi

- Menambahkan atribut `priority` pada struktur `proc` di `proc.h`
- Mengubah fungsi `scheduler()` di `proc.c` untuk memilih proses dengan prioritas tertinggi (angka terkecil) yang dalam status RUNNABLE
- Mengedit program uji `ptest.c` untuk membuat 3 proses (Parent, Child 1, Child 2) dengan prioritas berbeda
- Proses dengan prioritas tertinggi seharusnya selesai lebih dahulu sesuai algoritma Non-Preemptive Priority
---

## ✅ Uji Fungsionalitas

- `ptest`: untuk menguji urutan eksekusi proses berdasarkan prioritas

---

## 📷 Hasil Uji

Lampirkan hasil uji berupa screenshot atau output terminal.

### 📍 Output `ptest`:

```
Child 2 selesai
Child 1 selesai
Parent selesai
```

📷 Screenshot:

<img width="977" height="452" alt="image" src="https://github.com/user-attachments/assets/02f3cabd-5c94-453d-9020-a49ba84540f4" />


```
```
---

## ⚠️ Kendala yang Dihadapi

- Error `proc undeclared` karena masih menggunakan variabel global `proc` alih-alih `c->proc` di dalam `scheduler()`
- Error `p undeclared` saat memanggil `c->proc = p;` sebelum `p` dideklarasikan
- Kesalahan urutan inisialisasi pointer `p` sebelum loop menyebabkan error kompilasi
- Solusi: memindahkan deklarasi `struct proc *p;` ke atas sebelum digunakan

---

## 📚 Referensi

- Buku xv6 MIT: https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf
- Repositori xv6-public: https://github.com/mit-pdos/xv6-public
- Forum Diskusi Praktikum & Stack Overflow

---
