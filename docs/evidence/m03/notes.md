# Catatan Evidence M03

## Lingkungan
- Penyedia: Microsoft Azure (Azure for Students), region Korea Central
- VM: Standard B2ats v2, 2 vCPU, 1 GiB RAM, disk 60 GB
- Berbeda dari spesifikasi modul (1 vCPU / 1 GB / 20 GB), tetapi RAM sama
- Karena RAM sama, konfigurasi Gunicorn 1 worker + 2 thread dipertahankan
- OS: Ubuntu Server 24.04 LTS

## Temuan dan troubleshooting
1. File konfigurasi SSH dari cloud-init (50-cloud-init.conf) menyetel PasswordAuthentication yes, sehingga file modul (99-pti2802.conf) kalah urutan baca. Solusi: file diganti nama menjadi 00-pti2802.conf, lalu diverifikasi dengan sshd -T.
2. Port 80 harus dibuka di dua lapis: UFW di VPS dan Network Security Group di Azure.
3. Log Gunicorn menampilkan "Control server error" saat service start, tetapi aplikasi tetap melayani /health dengan HTTP 200. Dugaan: pengaman ProtectHome=true pada systemd. Belum diselidiki lebih lanjut.
4. Swap 1 GB ditambahkan sebagai safety buffer (langkah opsional modul).

## Batasan saat ini
- HTTP saja (HTTPS dikerjakan di M04)
- Satu VPS, tanpa database, tanpa container, deployment manual
