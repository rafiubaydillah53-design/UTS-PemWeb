# UTS Pemrograman Web - Analisis SQL Injection

Repositori ini berisi dokumentasi dan implementasi eksperimen keamanan web mengenai **SQL Injection (SQLi)** sebagai pemenuhan tugas UTS mata kuliah Pemrograman Web 2.

## Deskripsi Proyek
Proyek ini mendemonstrasikan bagaimana kerentanan *SQL Injection* dapat terjadi pada sistem autentikasi PHP dan MySQL, serta bagaimana cara memitigasinya menggunakan *Prepared Statements*. Eksperimen dilakukan dengan membandingkan dua implementasi form login: yang rentan (*vulnerable*) dan yang aman (*secure*).

## Struktur Repositori
- `koneksi.php` : Konfigurasi koneksi database.
- `login_vulnerable.php` : Skrip login yang sengaja dibuat rentan terhadap SQLi.
- `login_secure.php` : Skrip login yang sudah dimitigasi menggunakan *Prepared Statements*.

## Konfigurasi Database
Untuk menjalankan proyek ini, pastikan Anda telah membuat database dengan detail berikut:

1. Buat database baru bernama `db_uts_pemweb`.
2. Jalankan query berikut untuk membuat tabel:

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(50) NOT NULL
);

INSERT INTO users (username, password) VALUES ('admin', 'password123');
```

## Mekanisme Eksperimen
- **Skenario Serangan:** Pada `login_vulnerable.php`, input `' OR 1=1 #` digunakan untuk memanipulasi kueri SQL dan melewati autentikasi.
- **Skenario Mitigasi:** Pada `login_secure.php`, penggunaan *Prepared Statements* memastikan input pengguna diperlakukan sebagai data (literal), bukan perintah eksekusi SQL.

- ![Hasil Serangan](Screenshots/Screenshot(468).png)

## Informasi Penulis
- **Nama:** Rafi Ubaydillah
- **NIM:** 312410542
- **Kelas:** I241E
- **Mata Kuliah:** Pemrograman Web 2
- **Dosen Pengampu:** Agung Nugroho, S.Kom., M.Kom.
- **Institusi:** Universitas Pelita Bangsa

---
*Dibuat untuk keperluan tugas UTS mata kuliah Pemrograman Web 2.*
```
