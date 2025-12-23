# Quick Start

Pls create work directory.

EX)
```
mkdir ./UserName/work/mccwDocker
```

## 1. git clone
```
git clone https://github.com/Masamasamasashito/mcc-warmer
```

## 2. Get Ready .env
```
cp env.example .env
```

## 3. Generate security keys on .env (Crucial step!)

Run the command below for your OS in your terminal to append secrets to `.env`(You only need to do this once)


🍎 macOS / 🐧 Linux (Copy & Paste into Terminal)
```
echo "" >> .env
echo "N8N_ENCRYPTION_KEY=$(openssl rand -hex 32)" >> .env
echo "REQ_SECRET=$(openssl rand -hex 32)" >> .env
echo "POSTGRES_PASSWORD=$(openssl rand -base64 32 | tr -d '/+=')" >> .env
echo "REDIS_PASSWORD=$(openssl rand -base64 32 | tr -d '/+=')" >> .env
```

🪟 Windows PowerShell (Copy & Paste into PowerShell)
```
"" | Add-Content .env
$bytes = New-Object byte[] 32; (New-Object System.Security.Cryptography.RNGCryptoServiceProvider).GetBytes($bytes); $hex = -join ($bytes | ForEach-Object { $_.ToString("x2") }); "N8N_ENCRYPTION_KEY=$hex" | Add-Content .env
$bytes = New-Object byte[] 32; (New-Object System.Security.Cryptography.RNGCryptoServiceProvider).GetBytes($bytes); $hex = -join ($bytes | ForEach-Object { $_.ToString("x2") }); "REQ_SECRET=$hex" | Add-Content .env
$bytes = New-Object byte[] 32; (New-Object System.Security.Cryptography.RNGCryptoServiceProvider).GetBytes($bytes); $base64 = [Convert]::ToBase64String($bytes) -replace '[\/+=]', ''; "POSTGRES_PASSWORD=$base64" | Add-Content .env
$bytes = New-Object byte[] 32; (New-Object System.Security.Cryptography.RNGCryptoServiceProvider).GetBytes($bytes); $base64 = [Convert]::ToBase64String($bytes) -replace '[\/+=]', ''; "REDIS_PASSWORD=$base64" | Add-Content .env
```

## 4. Start Containers

```
docker compose up -d
```

> [!TIP]
> **Running Multiple Instances / Avoiding Port Conflicts**
> By default, ports are bound to `127.0.0.1` (localhost) to ensure security and reduce port conflicts on your host machine.
> You can customize this behavior or the specific ports used by editing the `.env` file (e.g., `DOCKER_HOST_BIND_ADDR`, `DOCKER_HOST_PORT_N8N_CONTAINER`).

### Production Setup (with Caddy)
To start with Caddy (Reverse Proxy), use the `prod` profile.
*Ensure `PRODUCTION=true` and valid domain/email settings in `.env` if enabling secure cookies/SSL.*

```
docker compose --profile prod up -d
```

## 5. n8n Launch Check

open : [http://localhost:5678](http://localhost:5678)
