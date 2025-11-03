# Bot-Start-infoLAN
# Raspberry Telegram Notifier

Questo progetto invia automaticamente messaggi su Telegram quando:

1. **Il Raspberry Pi si avvia** → messaggio con informazioni di rete (Ethernet o Wi-Fi, IP, gateway, MAC, uptime).
2. **Qualcuno si collega in SSH al Raspberry** → messaggio con utente, IP remoto e, se in LAN, MAC.

Tutto è gestito con **systemd**, quindi parte da solo ad ogni boot.

---

## Requisiti

- Raspberry Pi OS / Debian con `systemd`
- `curl` installato (di solito è già presente)
- Un bot Telegram (creato con **@BotFather**)
- Il tuo `CHAT_ID` (manda `/start` al bot e prendi l’id da `getUpdates`)

---

## Struttura del progetto

```text
.
├── /etc/telegram-boot-bot/
│   └── config.conf              # token e chat id
├── /opt/telegram-boot-bot/
│   └── notify_boot.sh           # script che invia il messaggio di avvio
└── /etc/systemd/system/
    ├── telegram-boot-bot.service        # servizio che parte al boot
    └── telegram-ssh-watcher.service     # servizio che resta in ascolto dei login SSH
