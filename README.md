# ECLYPSE Security Manager

**Advanced certificate management and network operations for ECLYPSE controllers**

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-lightgrey)]()

---

## 🚀 Features

- **🔐 Certificate Management**
  - Generate and deploy X.509 certificates
  - Multiple CA support
  - Automated certificate lifecycle management
  - Support for custom certificate fields and SANs

- **🌐 Network Discovery**
  - Automatic mDNS/Bonjour discovery
  - IP range scanning
  - Smart caching and validation

- **💾 Backup Operations**
  - Automated controller configuration backups
  - Local and remote backup management
  - Encrypted backup storage
  - Retention policies

- **📊 Reporting & Monitoring**
  - Certificate inventory with expiration tracking
  - Backup inventory and status
  - CSV and HTML report generation

- **⚙️ Cross-Platform**
  - Windows: Native `.exe` with embedded OpenSSL
  - Linux: Self-contained `.AppImage`
  - Encrypted profile system for secure credential storage

---

## 📦 Installation

### **Windows**

1. **Download** the latest `.exe` from [Releases](../../releases)
2. **Run** `ECLYPSE-Security-Manager-vX.X.XXXx.exe`
3. **First run:** OpenSSL extracts automatically (~5-10 seconds)
4. **Subsequent runs:** Instant

**Requirements:**
- Windows 10/11 (x64 or ARM64)
- No additional software needed

---

### **Linux**

1. **Download** the latest `.AppImage` from [Releases](../../releases)

2. **Make executable:**
   ```bash
   chmod +x ECLYPSE-Security-Manager-vX.X.XXXx.AppImage
   ```

3. **Run:**
   ```bash
   ./ECLYPSE-Security-Manager-vX.X.XXXx.AppImage
   ```

4. **(Optional) Install Avahi for automatic discovery:**
   ```bash
   # Fedora/RHEL:
   sudo dnf install avahi avahi-tools
   
   # Ubuntu/Debian:
   sudo apt install avahi-daemon avahi-utils
   ```

**Requirements:**
- Most Linux distributions (Ubuntu, Debian, Fedora, etc.)
- Fully self-contained (includes PowerShell + OpenSSL)

---

## 🔧 Quick Start

1. **Launch** the application
2. **Create or load a profile** (encrypted storage for your settings)
3. **Scan your network** for ECLYPSE controllers (mDNS or IP range)
4. **Generate a CA** (Certificate Authority) for signing
5. **Create certificates** for your controllers
6. **Deploy** certificates to controllers via API

**Detailed guides:** See [docs/](docs/) folder

---

## 🛠️ Building from Source

> **Note:** Source code is in a separate private repository. This repo is for releases only.

If you have access to the source repository:

### **Prerequisites**

**Windows:**
- PowerShell 7.0+
- PS2EXE module: `Install-Module ps2exe`

**Linux:**
- PowerShell 7.0+
- OpenSSL 3.x
- .NET SDK 8.0+

### **Build Commands**

```powershell
# Navigate to project
cd ECLYPSE-Security-Manager

# Run build script
pwsh build/ECY-Security-Manager-build-tools.ps1
```

**Output:** `releases/vX.X.XXXx/[platform]/`

---

## 📖 Documentation

- **[Installation Guide](docs/installation.md)** - Detailed setup instructions
- **[Quick Start Guide](docs/quick-start.md)** - Get started in 5 minutes  
- **[User Manual](docs/user-guide.md)** - Complete feature reference *(Coming soon)*
- **[Troubleshooting](docs/troubleshooting.md)** - Common issues and solutions *(Coming soon)*

---

## 📜 License

**ECLYPSE Security Manager** is licensed under the **GNU General Public License v3.0 (GPL-3.0)**.

### Your Code
- **License:** GPL v3
- **Copyright:** © 2025 Distech Controls - Advanced Technical Support
- **See:** [LICENSE](LICENSE) for full GPL v3 text

### Bundled Third-Party Components

This tool includes open-source components:

| Component | License | Usage |
|-----------|---------|-------|
| OpenSSL 3.5.4 | Apache License 2.0 | Certificate generation and signing |
| PowerShell 7.x (Linux) | MIT License | Linux AppImage runtime |
| PS2EXE | MIT License | Windows EXE compilation |

**Full Attribution:** [licenses/THIRD-PARTY-NOTICES.txt](licenses/THIRD-PARTY-NOTICES.txt)

**Compliance:**
- OpenSSL license included: `licenses/OPENSSL-LICENSE.txt`
- PowerShell license included: `licenses/POWERSHELL-LICENSE.txt`
- No source code modifications made to third-party components

---

## 🤝 Support

**Created by:** Robert Lastinger / Distech Controls Advanced Technical Support

**For support:**
- Check the [Issues](../../issues) tab for known problems
- Review [documentation](docs/)
- Contact Distech Controls Technical Support

---

## 🔐 Security

This tool handles sensitive credentials and certificates. Always:
- ✅ Use strong profile passwords
- ✅ Keep private keys secure
- ✅ Review generated certificates before deployment
- ✅ Use encrypted profile storage
- ⚠️ Never commit passwords or private keys to version control

---

## 🗺️ Roadmap

See [CHANGELOG.md](CHANGELOG.md) for version history and upcoming features.

---

**Made with ⚡ by Distech Controls Advanced Technical Support**
