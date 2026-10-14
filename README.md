# KulkasKu

Cloud Computing — PTI 2802
Pertemuan 3 — Project Inception

## Author
Nurul Aminatul / NIM 25832073013

## Problem
Anak kos dan mahasiswa perantau sulit mengingat tanggal kedaluwarsa bahan
makanan di kulkas sehingga makanan sering terbuang. KulkasKu mencatat bahan
makanan dan menandai yang paling dekat kedaluwarsa.

## Target Users
Anak kos, mahasiswa perantau, dan penghuni kos yang berbagi satu kulkas.

## Features M03
- baseline aplikasi Flask (halaman utama)
- health endpoint `/health`
- info endpoint `/api/info`
- deployment pertama di VPS

## Architecture

```mermaid
flowchart LR
    U[User] --> C[Caddy]
    C --> G[Gunicorn]
    G --> F[Flask]
```

## Infrastructure
- Azure VM Standard B2ats v2 (2 vCPU, 1 GiB RAM, 60 GB disk)
- Ubuntu Server 24.04 LTS
- Caddy, Gunicorn, systemd, UFW

## Public Endpoint
`http://20.194.5.217/`

## Health Check
`GET /health`

## Deployment
Lihat `docs/deployment.md`.

## Documentation
- `docs/requirements.md`
- `docs/architecture.md`
- `docs/adr/0001-initial-architecture.md`
- `docs/evidence/m03/`

## Security
- SSH key-only, root login nonaktif
- UFW dan Azure NSG aktif
- backend hanya listen di loopback
- tidak ada secret di repository

## Current Limitations
- HTTP saja
- belum ada database
- belum ada container
- deployment manual

## Roadmap
M04 DNS/HTTPS, M05 Data, M06 Container, M07 IaC, M09 CI/CD
