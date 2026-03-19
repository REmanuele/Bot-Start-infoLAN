# 🍓 Bot-Start-infoLAN (Raspberry Telegram Notifier)

This project automatically sends Telegram notifications for critical events on your Raspberry Pi:

1. **System Boot:** Sends a message with network information (Ethernet or Wi-Fi, IP, gateway, MAC address, uptime) as soon as the Raspberry Pi starts.
2. **SSH Login:** Sends an alert containing the username, remote IP, and (if on the LAN) the MAC address whenever someone connects via SSH.

Everything is managed via **systemd**, ensuring it runs automatically at every boot without manual intervention.

---

## 📋 Requirements

* **OS:** Raspberry Pi OS / Debian (or any Linux distribution with `systemd`).
* **Tools:** `curl` installed (usually pre-installed).
* **Telegram Bot:** A bot created via **[@BotFather](https://t.me/botfather)**.
* **Chat ID:** Your personal Telegram `CHAT_ID` (send `/start` to your bot and retrieve the ID via the `getUpdates` API).

---

## 📁 Project Structure


.
├── /etc/telegram-boot-bot/
│   └── config.conf              # Stores your Telegram Token and Chat ID
├── /opt/telegram-boot-bot/
│   └── notify_boot.sh           # Script that gathers info and sends the boot message
└── /etc/systemd/system/
    ├── telegram-boot-bot.service      # Service triggered at boot
    └── telegram-ssh-watcher.service   # Service listening for incoming SSH logins

---

## ⚙️ Installation & Setup

*(Add the commands needed to install and configure your scripts here. For example:)*

**1. Clone the repository:**
\`\`\`bash
git clone https://github.com/REmanuele/Bot-Start-infoLAN.git
cd Bot-Start-infoLAN
\`\`\`

**2. Configure the Bot:**
* Copy or create the configuration file in `/etc/telegram-boot-bot/config.conf`.
* Add your credentials:
  \`\`\`text
  TELEGRAM_TOKEN="your_bot_token_here"
  CHAT_ID="your_chat_id_here"
  \`\`\`

**3. Setup Scripts and Services:**
* Move `notify_boot.sh` to `/opt/telegram-boot-bot/` and make it executable:
  \`\`\`bash
  sudo chmod +x /opt/telegram-boot-bot/notify_boot.sh
  \`\`\`
* Move the `.service` files to `/etc/systemd/system/`.

**4. Enable and Start the Services:**
\`\`\`bash
sudo systemctl daemon-reload
sudo systemctl enable telegram-boot-bot.service
sudo systemctl enable telegram-ssh-watcher.service
sudo systemctl start telegram-ssh-watcher.service
\`\`\`

---

## 👨‍💻 Author

**Emanuele Rapisardi**
* [LinkedIn](http://www.linkedin.com/in/emanuele-rapisardi-a02844235)
* [Photography Portfolio](https://emanuelerapisardi.altervista.org/)
