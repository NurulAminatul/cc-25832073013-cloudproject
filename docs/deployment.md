# Manual Deployment M03

## Application Path
`/srv/cc-m03`

## Service
`cc-m03.service` (systemd)

## Backend
`127.0.0.1:8000` (Gunicorn, 1 worker, 2 thread)

## Reverse Proxy
Caddy pada port 80, konfigurasi di `/etc/caddy/Caddyfile`

## Public Endpoint
`http://20.194.5.217/`

## Update Procedure

```bash
cd /srv/cc-m03
git pull
source .venv/bin/activate
python -m pip install -r requirements.txt
sudo systemctl restart cc-m03
sudo systemctl status cc-m03 --no-pager
curl -fsS http://127.0.0.1:8000/health
curl -fsS http://127.0.0.1/health
```

Setelah itu uji dari client eksternal: buka `http://20.194.5.217/health`
di browser.

## Logs

```bash
sudo journalctl -u cc-m03 -n 50 --no-pager
sudo journalctl -u caddy -n 50 --no-pager
```

## Rollback Dasar

```bash
git log --oneline --decorate -10
git checkout m03
sudo systemctl restart cc-m03
git switch main
```

## Catatan
- Firewall berlapis: UFW di VPS dan Network Security Group di Azure.
- Login SSH hanya dengan key; password dan root login dinonaktifkan.
