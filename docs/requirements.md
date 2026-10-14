# Requirements — KulkasKu

## Problem Statement
Anak kos dan mahasiswa perantau mengalami kesulitan mengingat tanggal
kedaluwarsa bahan makanan di kulkas pada konteks tempat tinggal mandiri.
Sistem KulkasKu akan menyediakan pencatatan bahan makanan beserta penanda
sisa hari sebelum kedaluwarsa, sehingga bahan yang hampir basi dapat
dipakai lebih dulu dan pemborosan makanan berkurang.

## Target Users
- Anak kos / mahasiswa perantau yang menyimpan bahan makanan di kulkas
- Penghuni kos bersama yang berbagi satu kulkas
- Stakeholder: dosen pengampu (penilai), pengembang (mahasiswa)

## User Need
Sebagai anak kos,
saya ingin melihat bahan makanan yang paling dekat kedaluwarsa,
sehingga saya dapat memakainya lebih dulu dan tidak membuang makanan.

## Functional Requirements
- FR-01 Sistem menampilkan halaman utama. (M03, selesai)
- FR-02 Sistem menyediakan health endpoint /health. (M03, selesai)
- FR-03 Sistem menampilkan metadata aplikasi di /api/info. (M03, selesai)
- FR-04 Pengguna dapat menambah bahan makanan (nama, jumlah, tanggal kedaluwarsa). (rencana M05)
- FR-05 Sistem menampilkan daftar bahan, diurutkan dari kedaluwarsa terdekat. (rencana M05)
- FR-06 Sistem menandai status tiap bahan: aman, segera habiskan, atau kedaluwarsa. (rencana M05)
- FR-07 Pengguna dapat menghapus bahan yang sudah habis. (rencana M05)

## Non-Functional Requirements
- NFR-01 Backend hanya listen pada loopback (127.0.0.1).
- NFR-02 Aplikasi dikelola oleh systemd.
- NFR-03 Request publik masuk melalui reverse proxy (Caddy).
- NFR-04 Secret tidak disimpan pada Git repository.
- NFR-05 Health endpoint mengembalikan HTTP 200 saat sehat.
- NFR-06 Deployment dapat direproduksi dari repository.
- NFR-07 Arsitektur sesuai VPS dengan RAM 1 GiB.

## Scope
### In Scope M03
repository, requirements, architecture, ADR, baseline Flask app,
SSH hardening dasar, Gunicorn, systemd, Caddy, HTTP public deployment

### Out of Scope M03
database production, Docker, Infrastructure as Code, CI/CD,
TLS/domain production, horizontal scaling, monitoring stack penuh

## Constraints
- Azure VM Standard B2ats v2: 2 vCPU, 1 GiB RAM, disk 60 GB
- Ubuntu Server 24.04 LTS
- Public IPv4 (20.194.5.217)

## Acceptance Criteria M03
- [x] first deployment dapat diakses dari internet
- [x] health endpoint mengembalikan HTTP 200
- [x] SSH hanya dengan key, root login nonaktif
- [x] firewall (UFW dan Azure NSG) aktif
