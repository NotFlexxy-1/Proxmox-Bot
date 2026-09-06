# 🤖 hyperLXC BOT

### Proxmox VE LXC Management • Directly Inside Discord

**hyperLXC BOT** is a modern Discord-based management system for **Proxmox VE LXC containers**. It connects your Discord server directly to your Proxmox infrastructure, allowing administrators to provision, control, monitor, and manage VPS/LXC containers without constantly opening the Proxmox web interface.

Built with **Python, Discord.py, SQLite, and the Proxmox VE API**, hyperLXC BOT combines infrastructure automation with Discord's interactive UI components.

<p align="center">

**🚀 Deploy • 🖥️ Manage • 📊 Monitor • 🛡️ Protect • ⚡ Automate**

</p>

---

## ✨ Features

### 🖥️ VPS / LXC Management

hyperLXC BOT provides complete lifecycle management for registered LXC containers.

* 🚀 Create new LXC containers
* ▶️ Start containers
* ⏹️ Stop containers
* 🔄 Restart containers
* 🗑️ Delete containers
* ♻️ Reinstall operating systems
* 📏 Resize RAM
* ⚙️ Resize CPU
* 💾 Resize storage
* 📸 Create snapshots
* 🔙 Restore snapshots
* 📋 List snapshots
* 🔍 View detailed VPS information
* ⏱️ Check VPS uptime
* 📊 View live resource statistics

---

## 🧠 Proxmox VE Integration

hyperLXC BOT communicates directly with the **Proxmox VE API**.

Supported functionality includes:

* Proxmox node detection
* LXC provisioning
* VMID allocation
* LXC status management
* Resource configuration
* Storage configuration
* Network bridge configuration
* OS template discovery
* Proxmox user creation
* Proxmox ACL permissions
* Container snapshots
* Snapshot restoration
* Node statistics
* Container statistics

The bot uses a Proxmox API token for authentication.

```text
Discord
   │
   ▼
hyperLXC BOT
   │
   ▼
Proxmox VE API
   │
   ├── Node
   ├── Storage
   ├── LXC
   ├── Users
   ├── ACL
   └── Snapshots
```

---

# 🐧 Supported Operating Systems

The current deployment system supports:

| Operating System | Template                                      |
| ---------------- | --------------------------------------------- |
| 🟠 Ubuntu 22.04  | `ubuntu-22.04-standard_22.04-1_amd64.tar.zst` |
| 🟠 Ubuntu 24.04  | `ubuntu-24.04-standard_24.04-2_amd64.tar.zst` |
| 🔴 Debian 12     | `debian-12-standard_12.12-1_amd64.tar.zst`    |
| 🔴 Debian 13     | `debian-13-standard_13.1-2_amd64.tar.zst`     |

OS selection is performed through Discord's interactive dropdown UI.

---

# 🎛️ Interactive Discord Dashboard

hyperLXC BOT isn't limited to text-only commands.

It uses **Discord UI components** including:

* Dropdown menus
* Buttons
* Confirmation dialogs
* Interactive VPS selection
* Category-based help menus
* Ephemeral responses
* Interactive OS selection
* Refreshable dashboards

Example workflow:

```text
/create 4 2 40 @User
        │
        ▼
┌───────────────────────────────┐
│      VPS CREATION             │
│                               │
│  Select Operating System      │
│                               │
│  🟠 Ubuntu 22.04              │
│  🟠 Ubuntu 24.04              │
│  🔴 Debian 12                 │
│  🔴 Debian 13                 │
└───────────────────────────────┘
        │
        ▼
   Proxmox Deployment
        │
        ▼
    VPS Ready 🚀
```

---

# 📊 Live Resource Monitoring

The management dashboard can retrieve live information directly from Proxmox.

### CPU

```text
💻 CPU: 12.4%
```

### Memory

```text
🧠 Memory: 842MB / 4096MB (20.6%)
```

### Disk

```text
💾 Disk: 8.4GB / 40GB (21.0%)
```

### Uptime

```text
⏱️ Uptime: 3d 8h 21m
```

The management dashboard combines these metrics into a single Discord interface.

---

# 🛡️ Automated Resource Protection

hyperLXC BOT includes an automatic resource monitoring system.

The bot periodically scans running LXC containers and checks CPU usage against a configurable threshold.

Default threshold:

```text
CPU > 90%
RAM > 90%
```

When excessive CPU usage is confirmed, the bot can:

```text
High CPU detected
       │
       ▼
Double-check usage
       │
       ▼
Threshold exceeded
       │
       ▼
Container suspended
       │
       ▼
Database updated
       │
       ▼
Discord notification
```

This is designed to help detect potentially abusive workloads such as unauthorized mining activity.

Administrators can change thresholds dynamically.

```text
!thresholds
!set-threshold 90 90
```

---

# 👥 VPS Ownership & Sharing

Each VPS is associated with its Discord owner.

hyperLXC BOT supports sharing VPS access with other Discord users.

### Share a VPS

```text
!share-user @User 1
```

### Manage a shared VPS

```text
!manage-shared @Owner 1
```

### Revoke access

```text
!share-ruser @User 1
```

The system also creates Proxmox users for Discord users and applies LXC-specific ACL permissions.

---

# 🔐 User & Permission System

hyperLXC BOT includes multiple permission levels.

### Main Administrator

The main administrator is defined through:

```env
MAIN_ADMIN_ID=
```

The main admin can manage the administrative team.

### Additional Administrators

Administrators can be added and removed dynamically:

```text
!admin-add @User
!admin-remove @User
!admin-list
```

### VPS Users

Users who receive VPS instances can automatically receive a configurable Discord role.

```env
VPS_USER_ROLE_ID=
```

---

# 🧩 VPS Management Interface

The `manage` command provides an interactive VPS dashboard.

```text
!manage
```

The dashboard provides:

```text
┌────────────────────────────────────┐
│ 🖥️ VPS Dashboard                   │
├────────────────────────────────────┤
│ 🟢 VPS #1                          │
│ VMID: 101                          │
│ Ubuntu 24.04                       │
│ 4GB RAM • 2 CPU • 40GB Storage    │
├────────────────────────────────────┤
│ [▶️ Start] [⏹️ Stop]               │
│ [🖥️ Console] [📊 Stats]            │
│ [🔄 Reinstall] [🔃 Refresh]        │
└────────────────────────────────────┘
```

---

# 📸 Snapshot System

Administrators can create and restore LXC snapshots directly from Discord.

Create:

```text
!snapshot <container> <snapshot-name>
```

List:

```text
!list-snapshots <container>
```

Restore:

```text
!restore-snapshot <container> <snapshot-name>
```

Snapshots are executed through the Proxmox API.

---

# 📦 VPS Provisioning

Example:

```text
!create 4 2 40 @User
```

Parameters:

```text
RAM   = 4 GB
CPU   = 2 Cores
DISK  = 40 GB
USER  = Discord member
```

The bot then:

1. Generates the next Proxmox VMID.
2. Creates or finds the user's Proxmox account.
3. Locates the selected OS template.
4. Creates the LXC container.
5. Configures resources.
6. Configures networking.
7. Starts the container.
8. Grants Proxmox permissions.
9. Saves VPS information.
10. Assigns the VPS Discord role.
11. Sends credentials to the user by DM.

---

# 🔑 Automatic Credential Generation

During VPS deployment, hyperLXC BOT generates secure random passwords for container access.

Credentials can be sent privately through Discord DM rather than exposing them in public channels.

Example:

```text
🔐 Root Password
|| ************** ||

🔐 Panel Password
|| ************** ||
```

> Never share VPS credentials in public Discord channels.

---

# 💾 Local Database

The bot uses **SQLite** for persistent configuration and VPS management data.

Current database structures include:

```text
settings
vps
admins
```

The project also maintains JSON-based data files for:

```text
vps_data.json
admin_data.json
```

This allows the bot to preserve VPS ownership and administrative information across restarts.

---

# 📡 Server Statistics

Administrators can inspect Proxmox node resources using:

```text
!serverstats
```

The command reports:

* Host CPU usage
* Host memory usage
* Total registered VPS
* Proxmox node information

---

# 🔎 Proxmox Container Tools

Administrative commands include:

```text
!ct-list
!templates
!vpsinfo
!vps-uptime
```

These can be used to inspect the Proxmox environment and registered VPS instances.

---

# 🛠️ Resource Management

Administrators can dynamically modify VPS resources.

Example:

```text
!resize-vps hyperBOT-123456-1 8 4 80
```

This can modify:

```text
RAM     → 8 GB
CPU     → 4 Cores
Storage → 80 GB
```

Each change is also synchronized into the bot's VPS data.

---

# 🔄 Reinstall System

VPS owners can request an operating system reinstall from the interactive management panel.

The process includes:

```text
Confirm destructive action
        │
        ▼
Delete existing container
        │
        ▼
Select new OS
        │
        ▼
Deploy new container
        │
        ▼
Update VPS metadata
        │
        ▼
Send new credentials
```

⚠️ **Reinstalling destroys the existing container data.**

---

# 🎨 Modern Embed System

All major responses use a shared embed system with consistent branding.

Supported visual states include:

```text
🟢 Running
🔴 Stopped
🟡 Suspended
✅ Whitelisted
❓ Unknown
```

The project can use a custom HyperNET / hyperLXC logo throughout its Discord interface.

---

# 📚 Built-in Help System

The bot provides a category-based interactive help menu.

```text
!help
```

Categories include:

```text
👤 User
🖥️ VPS
🛡️ Admin
```

The help interface uses Discord dropdown components to make command discovery easier.

---

# ⚙️ Configuration

hyperLXC BOT uses environment variables for sensitive and deployment-specific settings.

Example:

```env
DISCORD_TOKEN=your_discord_bot_token

BOT_NAME=hyperLXC
PREFIX=!
YOUR_SERVER_IP=your.server.ip

MAIN_ADMIN_ID=123456789012345678
VPS_USER_ROLE_ID=123456789012345678

PROXMOX_URL=https://pve.example.com
PROXMOX_TOKEN_ID=root@pam!bot
PROXMOX_TOKEN_SECRET=your_proxmox_api_token
PROXMOX_NODE=pve

PROXMOX_STORAGE=local-lvm
PROXMOX_BRIDGE=vmbr0
```

---

# 📦 Requirements

Recommended environment:

```text
Python 3.10+
Proxmox VE
Discord Bot
SQLite
Internet access
```

Python dependencies include:

```text
discord.py
aiohttp
urllib3
```

---

# 🚀 Installation

Clone the repository:

```bash
git clone https://github.com/NotFlexxy-1/hyperLXC-BOT.git
cd hyperLXC-BOT
```

Create a virtual environment:

```bash
python3 -m venv venv
source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Configure environment variables:

```bash
nano .env
```

Then start the bot:

```bash
python3 bot.py
```

---

# 🤖 Discord Bot Permissions

The Discord application should have the permissions required for:

```text
Send Messages
Embed Links
Read Message History
Use Application Commands
Manage Roles
View Channels
Send Messages in Threads
```

For the current command implementation, message-content access is also required.

Enable the required intents in the Discord Developer Portal.

---

# 🔐 Proxmox API Requirements

Create a dedicated Proxmox API token for the bot.

Example:

```text
User:
root@pam

Token:
bot
```

Result:

```text
root@pam!bot
```

Configure:

```env
PROXMOX_TOKEN_ID=root@pam!bot
PROXMOX_TOKEN_SECRET=xxxxxxxx
```

The API token should only receive the permissions actually required by your deployment.

---

# 📋 Command Reference

## 👤 User Commands

| Command          | Description                   |
| ---------------- | ----------------------------- |
| `!ping`          | Check bot latency             |
| `!uptime`        | Show host uptime              |
| `!myvps`         | Show your VPS instances       |
| `!manage`        | Open VPS management dashboard |
| `!manage-shared` | Manage a shared VPS           |
| `!share-user`    | Share VPS access              |
| `!share-ruser`   | Revoke shared VPS access      |
| `!help`          | Open interactive help         |

---

## 🖥️ VPS Commands

| Command        | Description     |
| -------------- | --------------- |
| `!manage`      | VPS dashboard   |
| `!myvps`       | List owned VPS  |
| `!vps-uptime`  | Show VPS uptime |
| `!restart-vps` | Restart a VPS   |

---

## 🛡️ Administrator Commands

| Command             | Description                  |
| ------------------- | ---------------------------- |
| `!create`           | Create a VPS                 |
| `!delete-vps`       | Delete a VPS                 |
| `!delete-user`      | Delete a Proxmox user        |
| `!resize-vps`       | Resize VPS resources         |
| `!suspend-vps`      | Suspend VPS                  |
| `!unsuspend-vps`    | Unsuspend VPS                |
| `!serverstats`      | Show Proxmox node statistics |
| `!ct-list`          | List LXC containers          |
| `!templates`        | List templates               |
| `!snapshot`         | Create snapshot              |
| `!list-snapshots`   | List snapshots               |
| `!restore-snapshot` | Restore snapshot             |
| `!vpsinfo`          | Show VPS information         |
| `!resource-check`   | Run resource protection scan |
| `!thresholds`       | Show resource thresholds     |
| `!set-threshold`    | Configure thresholds         |
| `!set-status`       | Change bot presence          |

---

## 👑 Main Administrator Commands

| Command         | Description          |
| --------------- | -------------------- |
| `!admin-add`    | Add administrator    |
| `!admin-remove` | Remove administrator |
| `!admin-list`   | List administrators  |

---

# 🗂️ Project Structure

A recommended project structure:

```text
hyperLXC-BOT/
│
├── bot.py
├── requirements.txt
├── .env
├── vps.db
├── vps_data.json
├── admin_data.json
├── bot.log
├── README.md
└── LICENSE
```

---

# 📝 Logging

The bot writes logs to:

```text
bot.log
```

Logs are sent both to:

```text
File
└── bot.log

Console
└── stdout
```

This makes deployment troubleshooting significantly easier.

---

# 🔒 Security Notes

Do not commit secrets to GitHub.

Never expose:

```text
DISCORD_TOKEN
PROXMOX_TOKEN_SECRET
VPS passwords
API credentials
.env
```

Add the following to `.gitignore`:

```gitignore
.env
*.db
*.sqlite
bot.log
vps_data.json
admin_data.json
__pycache__/
venv/
```

For production deployments, use a dedicated Proxmox API account/token with the minimum permissions necessary.

---

# ⚠️ Important Production Notes

hyperLXC BOT directly controls infrastructure through Proxmox.

A compromised Discord administrator account or exposed API token could therefore affect your containers.

For production use, consider:

* Dedicated Proxmox API users
* Least-privilege ACLs
* Firewall restrictions
* Secure TLS certificates
* Secret management
* Regular database backups
* Discord administrator auditing
* Rate limiting
* Action logging

---

# 🚧 Roadmap

The project can evolve into a complete Discord-based VPS control platform.

Planned / future possibilities:

```text
✅ Proxmox LXC provisioning
✅ Interactive VPS dashboard
✅ Resource monitoring
✅ Snapshot management
✅ VPS sharing
✅ Automatic resource protection
✅ Admin management
✅ OS reinstall
✅ Resource resizing

⬜ Slash-command migration
⬜ Multi-node Proxmox clusters
⬜ IP address allocation
⬜ IPv4 / IPv6 management
⬜ Backup management
⬜ Scheduled backups
⬜ Scheduled power actions
⬜ Bandwidth monitoring
⬜ Network traffic statistics
⬜ Disk I/O monitoring
⬜ Web console integration
⬜ VNC / noVNC integration
⬜ Server billing integration
⬜ User quotas
⬜ VPS plans
⬜ Coupon / promotional system
⬜ Web dashboard
⬜ REST API
⬜ Webhooks
⬜ Audit log system
⬜ Advanced abuse detection
⬜ Automated backup rotation
⬜ Multi-server management
```

---

# 🌐 Vision

The goal of **hyperLXC BOT** is simple:

> **Turn Discord into a complete control center for Proxmox infrastructure.**

Instead of switching between:

```text
Discord
   ↓
Browser
   ↓
Proxmox
   ↓
Terminal
   ↓
Monitoring
```

hyperLXC aims to bring the management experience together:

```text
                 ┌───────────────────────┐
                 │       Discord         │
                 │                       │
                 │  hyperLXC BOT         │
                 └───────────┬───────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
          Provision       Monitor        Manage
              │              │              │
              └──────────────┼──────────────┘
                             ▼
                    ┌─────────────────┐
                    │   Proxmox VE    │
                    ├─────────────────┤
                    │ LXC Containers  │
                    │ Storage         │
                    │ Network         │
                    │ Users / ACL     │
                    │ Snapshots       │
                    └─────────────────┘
```

---

# ❤️ Built With

* 🐍 **Python**
* 🤖 **discord.py**
* 🖥️ **Proxmox VE API**
* 🌐 **aiohttp**
* 💾 **SQLite**
* 📦 **JSON**
* 🔐 **Secrets / secure credential generation**

---

# 📜 License

This project is intended for infrastructure management and automation.

See [`LICENSE`](LICENSE) for the full license terms.

---

# ⭐ Support the Project

If hyperLXC is useful to you:

⭐ Star the repository
🐛 Report bugs
💡 Suggest features
🔧 Submit improvements
📖 Improve the documentation

---

<p align="center">

### ⚡ hyperLXC BOT

**Proxmox infrastructure management, directly inside Discord.**

Made for the **HyperNET** ecosystem.

</p>
