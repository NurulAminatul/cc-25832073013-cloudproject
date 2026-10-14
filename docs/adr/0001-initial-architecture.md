# ADR-0001: Initial VPS Deployment Architecture

## Status
Accepted

## Context
Proyek KulkasKu perlu dideploy pada Azure VM Standard B2ats v2
(2 vCPU, 1 GiB RAM, 60 GB disk) dengan Ubuntu Server 24.04 LTS.
RAM yang terbatas menuntut stack yang ringan dan mudah dijelaskan.

## Decision
- Flask sebagai web framework
- Gunicorn 1 worker + 2 thread sebagai application server
- systemd sebagai service manager
- Caddy sebagai reverse proxy
- UFW dan Azure NSG sebagai firewall
- GitHub sebagai repository, deploy key sebagai akses VPS

## Alternatives
1. Node.js + PM2
2. NGINX + Gunicorn
3. Docker
4. PHP-FPM

## Rationale
- Python 3.12 sudah menjadi runtime default Ubuntu 24.04
- Gunicorn dapat di-bind ke loopback sehingga backend tidak terekspos
- Caddy sederhana dan siap dikembangkan ke HTTPS otomatis pada M04
- Docker belum dipakai karena containerization adalah capaian M06
- Konfigurasi 1 worker menjaga headroom RAM untuk SSH, systemd, dan Caddy

## Consequences
### Positive
- Stack ringan dan mudah dijelaskan
- Backend tidak terekspos langsung ke internet
### Negative
- Satu worker membatasi konkurensi
- Deployment masih manual

## Review Trigger
Ditinjau ulang pada M06/M07.
