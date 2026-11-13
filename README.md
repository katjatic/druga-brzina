# Druga Brzina – www.druga-brzina.si

Statična spletna stran. Vsebina je v mapi `public/`, brez build koraka.

## Lokalni predogled

    cd public && python3 -m http.server 8000

## Deploy

Vsak push na `main` sproži GitHub Action (`.github/workflows/deploy.yml`), ki z `rsync` preko SSH sinhronizira `public/` na Hetzner strežnik.

### GitHub Secrets (Settings → Secrets and variables → Actions)

| Secret | Opis |
|---|---|
| `HETZNER_HOST` | IP ali hostname strežnika |
| `HETZNER_USER` | SSH uporabnik (z pisalnim dostopom do ciljne mape) |
| `HETZNER_SSH_KEY` | zasebni SSH ključ (celotna vsebina) |
| `HETZNER_PORT` | neobvezno, privzeto 22 |
| `HETZNER_PATH` | neobvezno, privzeto `/var/www/druga-brzina` |

### Priprava strežnika

    sudo mkdir -p /var/www/druga-brzina && sudo chown DEPLOY_USER: /var/www/druga-brzina

Primer konfiguracije spletnega strežnika (Caddy, samodejni HTTPS): `deploy/Caddyfile`.
DNS: A (in AAAA) zapis za `druga-brzina.si` in `www.druga-brzina.si` na IP strežnika.
