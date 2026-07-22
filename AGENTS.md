# Deploy VPN-Bot + OpenVPN Server

Разверни связку Telegram-бота для управления OpenVPN через Docker.

## Состав

- `docker-compose.yml` — 2 сервиса: `ovpn-server` (kylemanna/openvpn) и `vpn-bot` (Python Telegram bot)
- `Dockerfile` — образ для бота (Python + Docker CLI + pyTelegramBotAPI)
- `vpn_bot.py` — код бота (команды `/start`, `/random` для генерации .ovpn конфигов)
- `.env` — переменные: `BOT_TOKEN`, `ADMIN_TELEGRAM_ID`, `OVPN_PORT`
- `openvpn-data/` — полная PKI (CA, сертификаты, ключи, конфиги OpenVPN)

## Что нужно сделать

### 1. Установить Docker и docker compose plugin

```bash
# Если не установлены:
apt-get update && apt-get install -y docker.io docker-compose-v2
```

### 2. Обновить IP сервера

В файле `openvpn-data/ovpn_env.sh` заменить `91.184.240.7` на реальный IP нового сервера:

- `OVPN_CN=<НОВЫЙ_IP>`
- `OVPN_SERVER_URL=udp://<НОВЫЙ_IP>:1194`

Это важно, чтобы сгенерированные .ovpn файлы указывали на правильный сервер.

### 3. Настроить .env

Проверить/заменить в `.env`:

- `BOT_TOKEN` — токен Telegram-бота (обязательно)
- `ADMIN_TELEGRAM_ID` — твой Telegram ID
- `OVPN_PORT` — порт OpenVPN (по умолчанию 1194)

### 4. Запустить

```bash
docker compose up -d
```

### 5. Проверить

```bash
docker compose logs bot
docker compose logs vpn
```

Бот должен ответить на команды `/start` или `/random` в Telegram.
