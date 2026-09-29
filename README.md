# ONEX VPN Panel v1.3.9

**Advanced VPN Configuration Management & Distribution Platform**

A powerful, modern panel for managing VLESS, Trojan, and subscription-based VPN configurations with built-in traffic monitoring, user management, and Telegram bot integration.

---

## 📋 Features

### Core Management
- 🔐 **Multi-Protocol Support**: VLESS, Trojan, Hysteria2, Tuic, ShadowSocks, SOCKS5, HTTP, and more
- 📊 **Real-time Statistics**: Live traffic monitoring, connection tracking, bandwidth usage
- 👥 **User Management**: Create, edit, delete configurations with granular control
- 🎛️ **Advanced Filters**: Group by protocol, status, expiry, traffic usage
- ⏱️ **Expiration Management**: Auto-expire configs, set traffic limits and bandwidth caps
- 🔄 **Subscription System**: Generate subscription URLs with automatic config distribution

### Dashboard
- 🎨 **Modern UI**: Glass-morphism design with smooth animations
- 🌙 **Dark/Light Theme**: Customizable color schemes (Aurora, Lime, Rose, Emerald, Violet, Gold)
- 📱 **Fully Responsive**: Optimized for desktop, tablet, and mobile
- 📈 **Live Charts**: Traffic graphs, uptime tracking, connection metrics
- 🔔 **Real-time Notifications**: Update alerts and system notifications

### Security & Administration
- 🛡️ **Role-based Access**: Admin permission levels for security
- 🔑 **Session Management**: Secure token-based authentication
- 📝 **Activity Logging**: Comprehensive audit trail of all actions
- 🚀 **One-click Updates**: Auto-deploy new versions via Railway
- 📱 **Telegram Bot Integration**: Manage configs via @botfather integration

### Advanced Features
- 🌐 **Domain Grouping**: Organize configs into groups with shared URLs
- 📤 **Bulk Operations**: Create, update, delete multiple configs at once
- 🔍 **IP Limiting**: Restrict connections per IP address
- 🚦 **Speed Limiting**: Bandwidth throttling per config
- 📅 **Scheduled Management**: Auto-disable expired configs
- 💾 **Backup & Restore**: Full backup of all data and bot settings

---

## 🚀 Quick Start

### Prerequisites
- **Python** 3.9+
- **pip** (Python package manager)
- **Railway** account (for cloud deployment) or any VPS

### Local Installation

```bash
# Clone or extract the project
cd ONEX-main

# Install dependencies
pip install -r requirements.txt

# Run the application
python app.py
```

Access the panel at: `http://localhost:8000`
- **Default Username**: `admin`
- **Default Password**: `admin`

⚠️ **Change the default password immediately after first login!**

---

## ☁️ Railway Deployment (Recommended)

### Step 1: Prepare for Railway
```bash
# Create a Procfile (if not exists)
echo 'web: python app.py' > Procfile

# Create .railwayignore (skip unnecessary files)
echo 'archive/
docs/
frontend/
*.bak
all.js
all_unescaped.js' > .railwayignore
```

### Step 2: Deploy on Railway
1. Go to [railway.app](https://railway.app)
2. Click **"New Project"** → **"Deploy from GitHub"**
3. Select your ONEX repository
4. Railway auto-detects Python and installs dependencies
5. Set environment variables:
   ```
   PORT = 8000 (default)
   RAILWAY_VOLUME_MOUNT_PATH = /data (for persistent storage)
   ```
6. Your panel is live! 🎉

### Step 3: Configure Telegram Bot (Optional)
1. Message [@BotFather](https://t.me/BotFather) on Telegram
2. Create a new bot and copy the **Token**
3. In ONEX Panel → **ربات ONEX** → Paste token
4. Enable **Webhook** (auto-configured on Railway)
5. Use bot commands:
   - `/start` - View your configs
   - `/status` - Check usage and expiry
   - `/help` - Available commands

---

## 📖 Full Documentation

### Dashboard Sections

#### 1. **داشبورد (Dashboard)**
Main overview showing:
- 📊 Active connections and total traffic
- 📈 Real-time bandwidth usage charts
- ⏫ Server uptime and system status
- 📱 Recent activity log
- 🔄 Quick actions and shortcuts

#### 2. **کانفیگ‌ها (Configs)**
Create and manage individual VPN configurations:

**Create Config:**
- **Name**: Unique identifier for the config
- **Protocol**: Choose from supported protocols
- **Traffic Limit**: GB/TB limit (0 = unlimited)
- **Expiry Days**: Auto-disable after X days (0 = never)
- **IP Limit**: Max concurrent IPs (0 = unlimited)
- **Speed Limit**: Max bandwidth per connection (Mbps)

**Status Colors:**
- 🟢 **Green**: Active, within limits
- 🟡 **Yellow**: Nearing expiry or traffic limit
- 🔴 **Red**: Expired or exceeding limits

#### 3. **گروه‌ها (Groups)**
Organize configs into subscription groups:
- Share multiple configs under one subscription URL
- Custom group names and metadata
- Generate shareable QR codes
- Track group-level statistics

**Example:**
- Group: "Premium Users"
- Contains: 5 VLESS configs + 3 Trojan configs
- Share URL: `https://panel.example.com/sub/group-abc123`

#### 4. **آمار (Statistics)**
Time-based analytics with filters:
- **Traffic Analysis**: Data usage per day/week/month
- **Connection Tracking**: Active users and peak times
- **Protocol Distribution**: Usage breakdown by protocol
- **Geographic Data**: Connection sources (if available)

#### 5. **لاگ فعالیت (Activity Logs)**
Complete audit trail showing:
- Who created/modified configs
- When actions were taken
- IP addresses of administrators
- System errors and warnings
- Export logs as CSV

#### 6. **ربات ONEX (Telegram Bot)**
Manage configs through Telegram:
- **Users Tab**: List all bot users and activity
- **Broadcast**: Send messages to all users
- **Settings**: Configure bot token and webhooks
- **Commands**: Define custom bot behavior

#### 7. **تم و ظاهر (Theme)**
Customize the panel appearance:
- **Color Schemes**: 6 pre-built themes + custom colors
- **Dark/Light Mode**: System-aware or manual toggle
- **Language**: فارسی (Persian) or English
- All settings saved in browser

#### 8. **تنظیمات (Settings)**
Administration and configuration:
- **Change Password**: Update admin credentials
- **Backup & Restore**: Download/upload all data
- **Security**: Session management, IP blocking
- **System Info**: App version, database status

---

## 🔌 Supported Protocols

| Protocol | Type | Use Case | Speed |
|----------|------|----------|-------|
| **VLESS** | Modern | Default choice, fastest | ⚡⚡⚡ |
| **Trojan** | Legacy | Compatibility, masking | ⚡⚡ |
| **Hysteria2** | UDP | High-speed UDP, gaming | ⚡⚡⚡ |
| **Tuic** | QUIC | Low-latency streaming | ⚡⚡⚡ |
| **ShadowSocks** | Proxy | Legacy support, simple | ⚡ |
| **SOCKS5** | Proxy | Universal compatibility | ⚡ |
| **HTTP** | Proxy | Basic proxy support | ⚡ |
| **VMess** | Legacy | Old client support | ⚡ |

**Recommended**: VLESS-WS for reliability, Hysteria2 for speed

---

## 📋 Configuration Parameters

### Traffic Limits
```
0 = Unlimited
1 = 1 GB
100 = 100 GB
1000 = 1 TB
```

### Speed Limits
```
0 = Unlimited
1 = 1 Mbps (128 KB/s)
100 = 100 Mbps (12.5 MB/s)
1000 = 1 Gbps (125 MB/s)
```

### Expiry Options
```
0 = Never expires
1 = Expires in 1 day
30 = Expires in 30 days
365 = Expires in 1 year
```

### IP Limiting
```
0 = Unlimited concurrent IPs
1 = 1 IP only
5 = Up to 5 different IPs
```

---

## 🔄 Subscription URLs

### Individual Config
```
https://panel.example.com/sub/{uuid}
```
Returns VLESS link in subscription format.

### Group Subscription
```
https://panel.example.com/sub-group/{group-uuid}
```
Returns multiple configs for the group.

### All Configs
```
https://panel.example.com/sub-all
```
Returns all available configs (public or filtered).

**Import in Client:**
- Copy subscription URL
- Open VPN client (Clash, V2RayN, etc.)
- Add subscription source
- Auto-update configs periodically

---

## 🛠️ API Endpoints

### Authentication
```
POST /api/login
POST /api/logout
POST /api/change-password
```

### Configs
```
GET /api/links
POST /api/links
POST /api/links/delete
PUT /api/links/{uid}
GET /api/links/{uid}/info
```

### Groups
```
GET /api/subs
POST /api/subs
POST /api/subs/{sub_id}/links
```

### Statistics
```
GET /api/activity
GET /api/connections
GET /stats
```

### Admin
```
GET /api/admins
POST /api/admins
POST /api/security/sessions/revoke
```

### System
```
GET /api/system/metrics
POST /api/update/deploy
GET /api/update/check
```

---

## 🔒 Security Best Practices

1. **Change Default Password**: Do this immediately after installation
2. **Enable HTTPS**: Use a reverse proxy (nginx, Cloudflare)
3. **Backup Regularly**: Download backups weekly
4. **Monitor Logs**: Check activity logs for suspicious behavior
5. **Use Strong Passwords**: Min 12 characters, mixed case, numbers, symbols
6. **Session Timeout**: Set appropriate timeout periods
7. **IP Whitelisting**: Restrict admin access to trusted IPs
8. **Regular Updates**: Enable auto-update feature

---

## 📱 Mobile Access

The panel is fully responsive and works on:
- **iOS**: Safari, Chrome mobile
- **Android**: Chrome, Firefox mobile
- **Tablets**: Full desktop experience

No separate app needed – everything works through the web!

---

## 🐛 Troubleshooting

### Panel Won't Start
```bash
# Check Python version
python --version  # Should be 3.9+

# Install missing dependencies
pip install --upgrade -r requirements.txt

# Check if port 8000 is available
lsof -i :8000
```

### Can't Create Configs
- Check admin permissions
- Ensure server has available resources
- Verify database connectivity

### Telegram Bot Not Working
- Confirm bot token is correct (no spaces)
- Check webhook settings in panel
- Verify Railway webhook URL in bot settings

### Slow Performance
- Check server resources (CPU, RAM, disk)
- Enable caching in reverse proxy
- Reduce chart data retention
- Use CDN for static assets

---

## 📞 Support & Community

- **Issues**: Report bugs via GitHub Issues
- **Telegram**: [@V2rayTun0](https://t.me/V2rayTun0) - Main channel
- **Documentation**: See README.fa.md for Persian docs

---

## 📄 License

This project is provided as-is for educational and personal use.

---

## 🚀 Version History

| Version | Date | Changes |
|---------|------|---------|
| **1.3.9** | Sep 2026 | UI fixes, notification panel, auto-update |
| 1.3.8 | Aug 2026 | Theme customization, Telegram integration |
| 1.3.0 | Jul 2026 | Dashboard redesign, protocol support |

---

**Happy VPN Managing! 🎉**

For the best experience, deploy on Railway and enable all features.
