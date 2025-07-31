# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi  
**Semester**: Genap / Tahun Ajaran 2024–2025  
**Nama**: Novi Fitriyani  
**NIM**: 240202843  
**Modul yang Dikerjakan**: Modul 3 — Manajemen Memori Tingkat Lanjut (xv6-public x86)  


---

## 📌 Deskripsi Singkat Tugas

**Modul 3 – Manajemen Memori Tingkat Lanjut**  
Pada modul ini dilakukan dua eksperimen besar terkait manajemen memori dalam xv6, yaitu:
- Implementasi Copy-on-Write Fork (CoW) untuk meningkatkan efisiensi fork()
- Implementasi Shared Memory ala System V, yaitu shmget(key) dan shmrelease(key) untuk berbagi memori antar proses
---

## 🛠️ Rincian Implementasi


###  Copy-on-Write Fork

- Mengubah fungsi fork() di proc.c agar menggunakan teknik copy-on-write.
- Menambahkan bit PTE_COW di mmu.h untuk menandai page yang dibagi read-only.
- Menambahkan handler khusus di trap.c untuk menangani page fault akibat CoW.
- Menambahkan fungsi incref() dan decref() untuk reference count per page.
- Memodifikasi walkpgdir() agar mendukung flag CoW.
- Memastikan exit() dan wait() melakukan decrement ref_count yang benar.

### Shared Memory ala System V
- Menambahkan dua syscall baru shmget(int key) dan shmrelease(int key) di sysproc.c dan usys.S.
- Menambahkan struktur shmtab[] sebagai tabel shared memory di vm.c.
- Shared memory dipetakan ke alamat virtual dari USERTOP ke bawah.
- Menambahkan proses remapping ulang di fork() agar anak tetap bisa mengakses shared memory.
  
---

## ✅ Uji Fungsionalitas

* cowtest: untuk menguji fork dengan Copy-on-Write
* shmtest: untuk menguji shmget() dan shmrelease()

---

## 📷 Hasil Uji

Lampirkan hasil uji berupa screenshot atau output terminal.

### 📍 Output `cowtest`:

```
Child sees: Y
Parent sees: X
```

### 📍 Output `shmtest`:

```
Child reads: A
Parent reads: B
```

📷 Screenshot:

<img width="1028" height="433" alt="image" src="https://github.com/user-attachments/assets/4c5f7a43-6f2d-40cc-9bf1-86d5998c5630" />



```

---

## ⚠️ Kendala yang Dihadapi

- Implementasi awal CoW menyebabkan panic saat page fault karena salah akses bit flag PTE
- Beberapa halaman tidak di-set CoW dengan benar karena kesalahan logika duplikasi PTE
- Alamat virtual shared memory yang dipetakan ke USERTOP sempat berbenturan dengan area stack
- Child process gagal mengakses shared memory karena fork() belum melakukan remap shm

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---
