
---

# ECLYPSE Security Manager

> ⚠️ **IMPORTANT: COMMUNITY TOOL - NOT AN OFFICIAL DISTECH CONTROLS PRODUCT**
>
> This application is a special project developed by the Distech Controls Advanced Support Team and is **NOT a sanctioned or official release** by Distech Controls. Please read the **[DISCLAIMER.txt](DISCLAIMER.txt)** before using this tool.

**Enterprise-grade certificate lifecycle management and network operations for ECLYPSE Building Automation Systems**

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-lightgrey)]()
[![PowerShell](https://img.shields.io/badge/PowerShell-7.0%2B-blue)]()
[![OpenSSL](https://img.shields.io/badge/OpenSSL-3.x-green)]()
[![Community Tool](https://img.shields.io/badge/status-community%20tool-orange)]()

---

## ⚠️ Important Notice

**THIS IS A COMMUNITY TOOL - READ BEFORE USE**

This application is:
- ✅ **Freely available** for use and redistribution
- ✅ **Built using** only publicly available RESTful API endpoints
- ✅ **Supported by Advanced Support** at their discretion, primarily for Distech SI's, Distributors, OEMs, and partners
- ❌ **NOT an official Distech Controls product**
- ❌ **NOT covered** by Distech Controls warranties or support agreements
- ❌ **NOT subject** to standard Distech Controls release procedures

**📋 [READ THE FULL DISCLAIMER](DISCLAIMER.txt)** - Contains important legal information about warranty, liability, and support.

**By using this tool, you acknowledge and accept these terms.**

---

## 🔄 Semantic Versioning Adoption

**Version Numbering:** v6.17.399b → v1.0.1 → v1.0.7 → v1.0.8 → v1.0.9

We've transitioned from development versioning (6.x.x) to **semantic versioning** for clearer release communication:

- **MAJOR** (1.x.x): Breaking changes requiring user action
- **MINOR** (x.1.x): New features, backward compatible
- **PATCH** (x.x.1): Bug fixes and improvements

**This is NOT a downgrade** - v1.0.9 is **NEWER** than v6.17.399b and includes all features plus Network Interface Management, Event Management, and Task Automation. The built-in update checker correctly detects these transitions.

**Upgrading from v6.17.x, v1.0.1, v1.0.7, or v1.0.8?** Your profiles are fully compatible. Just replace the executable/AppImage - no migration needed.

---

## 🎯 What is This?

ECLYPSE Security Manager is a **complete PKI and network management solution** designed specifically for ECLYPSE controllers in Building Automation Systems. It streamlines certificate lifecycle management, automates routine tasks, and provides enterprise-level security features for BAS environments ranging from single-site installations to large distributed deployments.

**Built for:** System integrators, IT administrators, and support engineers managing ECLYPSE controllers

**Developed by:** Distech Controls Advanced Support Team (community project)

**Replaces:** Manual certificate generation, ad-hoc OpenSSL commands, spreadsheet-based controller tracking

---

<details>
<summary><b>🖼️ Click to view application screenshots</b></summary>

### Profile Selection
![Profile Selection](images/profile-selection.png)
*Secure, encrypted profiles with multi-user support*

### Main Dashboard
![Main Menu](images/main-menu.png)
*Intuitive menu-driven interface for all operations*

### Network Discovery
![mDNS Discovery](images/mdns-discovery.png)
*Automatic controller discovery using mDNS/Avahi*

### Backup Management
![Backup Dashboard](images/backup-dashboard.png)
*Visual dashboard with bar charts for backup status*

### Certificate Inventory
![Certificate Inventory](images/certificate-inventory.png)
*Comprehensive certificate tracking across all controllers*

</details>

---

## ✨ Key Features

### 📬 **Event Management (Enhanced in v1.0.9)**

- **Recipient Management:** View and delete MQTT, Email, and Webhook recipients
  - Parallel querying across all controllers
  - Type display: MQTT brokers, Email SMTP, HTTP/HTTPS webhooks
  - Connection details: Topic, connection string, QoS settings
  - Intelligent deduplication across controllers

- **Task Management:** View, create, and delete scheduled tasks and automation
  - **Task Creation (NEW in v1.0.9):** 8-step wizard for scheduled controller reboots
    - Guided cron expression builder (Hourly, Daily, Weekly, Monthly, Custom)
    - Frequency enforcement (minimum 1-hour interval)
    - Optional task expiration with automatic self-cleanup
    - Recipient override capability
    - Parallel task creation across multiple controllers
  - **Multi-Task Deletion (NEW in v1.0.9):** Delete multiple tasks at once
    - Single selection: `1`
    - Range selection: `1-3`
    - List selection: `1,3,5`
    - Automatic duplicate removal
  - Task status: Enabled/disabled state with visual indicators
  - Action details: HTTP method, endpoint URLs
  - Execution history: Last status (Success/Failed) with timestamps
  - Trigger and recipient associations

- **Task Expiration with Self-Cleanup:**
  - Creates expiration task that deletes main task AND itself
  - Uses batch API: `POST /api/rest/v2/batch`
  - Dual DELETE operations in escaped JSON body
  - Single trigger execution removes both tasks automatically
  - No manual cleanup required

- **Batch Deletion Operations:**
  - Parallel scanning to identify unique items
  - Controller count display (e.g., "Found on: 8/12 controllers")
  - Typed confirmation for safety ("DELETE" required)
  - 3-pass retry with adaptive throttling
  - Smart verification: Items not found = success (desired state)

- **Use Cases:**
  - **NEW:** Schedule maintenance reboots (daily, weekly, monthly)
  - **NEW:** Time-limited automation (task expires after project completion)
  - **NEW:** Bulk cleanup of old/test automation tasks
  - Clean up test/demo MQTT configurations
  - Remove deprecated webhook integrations
  - Audit event configurations across sites
  - Prepare controllers for new integrations
  - Troubleshoot event delivery issues

### 🌐 **Network Interface Management (v1.0.7)**

- **View Interface Status:** Real-time IPv4/IPv6 configuration monitoring
  - Bridge, primary, secondary interface support
  - Operational status: Routable, Carrier, NoCarrier, Off
  - IP address display with color-coded status indicators
  - Bulk queries across all controllers

- **Configure IPv4/IPv6 Settings:** Batch operations with enterprise reliability
  - 6 action options: Enable/disable IPv4, IPv6, or both
  - Multi-interface selection (comma-separated: "1,2" for primary+secondary)
  - Typed confirmation for safety ("CONFIRM" required)
  - Automatic verification scan after changes

- **3-Pass Retry System:** Intelligent failure recovery
  - Pass 1: Attempt all controllers
  - Pass 2: Retry failures from Pass 1
  - Pass 3: Final retry for persistent failures
  - **Result:** 97-99% success rate vs 85-90% single-pass
  - Silent retries with final summary (✓/✗ per controller)
  - Real-time progress: `⚡ Pass 2 : 5/10 (50%) | controller-01 | ETA: 45s`

- **Adaptive Network Integration:** Dynamic operation tuning
  - Pre-operation network quality detection (5-sample latency test)
  - Delay adjustment based on conditions (Excellent/Good/Fair/Poor/Critical)
  - Automatic throttle increases on failures (reliability over speed)
  - Live metrics: Avg latency, packet loss %, quality badge

### 🔐 **Advanced Certificate Management**

- **Multi-CA Architecture:** Manage multiple Certificate Authorities simultaneously with intelligent selection
- **Custom Certificate Builder:** 8-step wizard with full control over extensions, SANs, and key usage
- **CSR Workflow:** Generate Certificate Signing Requests for external CA signing with automatic import matching
- **16 Export Formats:** PKCS#12, PEM, DER, JKS, PKCS#8, and specialized formats (EC-Net/Niagara bundles)
- **Certificate Templates:** Save and reuse certificate configurations
- **Variable Expansion:** Batch generate certificates with patterns (`controller{+1}`, `device-{001}`)
- **Expiration Tracking:** Automated monitoring with configurable warning periods
- **3-Pass Deployment:** Matches interface management reliability

### 🌐 **Intelligent Network Discovery**

- **Hybrid mDNS:** Avahi (Linux), Bonjour (Windows), and native .NET fallback
- **Smart Caching:** Skip validation for recently-scanned controllers (60-80% faster repeat scans)
- **TCP Pre-Flight:** Filter dead IPs before HTTPS validation (saves 4.5s per dead IP)
- **Parallel Scanning:** Configurable thread count (1-50 threads) with adaptive performance
- **IPv6 Optimization:** Automatic adapter management with hybrid restoration
- **Metadata Pre-Loading:** Batch API calls fetch backup/cert counts in parallel

### 💾 **Comprehensive Backup System**

- **Remote Backup Operations:**
  - Create, download, and delete backups via controller API
  - Granular selection: All/Latest/By-Age/By-Count/Specific
  - Overwrite behavior control (skip existing vs force re-download)
  - 3-pass retry for reliability

- **Local Backup Management:**
  - Profile-based organization (`Backups/{Profile}/{Controller}/`)
  - Optional AES-256 encryption with profile password
  - Date-based filtering and bulk operations
  - Automated retention policies

- **Backup Dashboard:** Real-time status with coverage metrics and bar chart visualization

### 👤 **Profile & Session Management**

- **Encrypted Profiles:**
  - AES-256-CBC with PBKDF2 key derivation (10,000 iterations)
  - Per-profile password protection (separate from session credentials)
  - Controller lists, CAs, jobs, and settings stored encrypted

- **Profile Export/Import:**
  - Portable encrypted packages with integrity validation
  - HMAC-SHA256 signature + SHA256 per-file checksums
  - Selective component inclusion (CAs, certificates, backups, job templates)
  - Cross-profile security (re-encryption with target password)
  - Comprehensive audit logging

- **Session Management:**
  - Configurable timeout with lock/logout actions
  - Operation protection (suspend timeout during backups/scans)
  - Warning countdown (2-minute alert before timeout)
  - Inactivity tracking with automatic reset

- **Profile Locking:**
  - Multi-instance protection with stale detection
  - Process ID tracking (crash recovery)
  - Automatic lock file cleanup
  - Override options for legitimate concurrent access

### ⚙️ **Background Job System**

- **Automated Execution:**
  - Timer-based job execution (checks every minute)
  - Sequential queue processing prevents conflicts
  - Smart catch-up (missed jobs execute on restart)

- **Job Types:**
  - Remote Backup (download with advanced filters)
  - Remote Backup Create (scheduled backup creation)
  - Remote Backup Cleanup (age-based remote deletion)
  - Local Cleanup (retention policy enforcement)
  - Certificate Renewal (planned for v1.1.0)
  - Network Scan (planned for v1.1.0)

- **Scheduling Options:**
  - Daily, Weekly, Monthly
  - Hourly intervals
  - Minute intervals (5-1440 min)
  - Manual/on-demand

- **Job Management:**
  - Real-time dashboard with countdown timers
  - Execution history with retention policies
  - Enable/disable toggles
  - Manual execution triggers

### 🗂️ **Controller Management**

- **Dashboard View:** Summary-first design for 100+ controller environments
- **Submenu Structure:**
  - Option 1: Controller Dashboard
  - Option 2: Network Interface Management
  - Option 3: Event Management (Task Creation in v1.0.9)
  - Clear navigation labels
- **Per-Controller Credentials:** Override session credentials for specific controllers (encrypted)
- **Metadata Caching:** Operation-aware cache with configurable TTL (10-60 minutes)
- **Bulk Operations:** Filter-based actions (no backups, no CA, no certs, by age)
- **Validation Tools:** Parallel connectivity testing with reachability reports

### 📊 **Dual-Channel Modular Logging**

- **Two Independent Channels:**
  - File Output: Persistent log files (default: WARNING level)
  - Console Output: Real-time display (default: ERROR level)

- **Five Verbosity Levels:** ERROR < WARNING < INFO < DEBUG < TRACE
- **Per-Module Overrides:** Separate verbosity for Scanning, Certificates, Backups, General, Events
- **Quick Presets:** Troubleshooting, Production, Development, Silent modes
- **Silent Mode:** Retry operations log at DEBUG level (file-only)

### 🔒 **Security Features**

- **Licensing System:**
  - Time-limited builds (30/60/90/180/365 day validity)
  - Password-protected licenses (optional)
  - CA-signed certificates with signature validation
  - Embedded license PFX in compiled binaries
  - Expiration enforcement with countdown warnings

- **Credential Management:**
  - 3-tier storage (session/profile/don't save)
  - Certificate passwords cached for batch operations
  - Controller credentials saved encrypted in profile
  - Per-controller credential overrides
  - Per-operation credential prompts with reuse option

- **Encryption:**
  - Profile data: AES-256-CBC with PBKDF2
  - Backup files: Optional AES-256 encryption
  - Private keys: Always encrypted (AES-256 or PKCS#8)

### 🚀 **Performance Optimizations**

- **Parallel Operations:**
  - RunspacePool-based multi-threading (configurable 1-50 threads)
  - Batch API calls (75% faster than sequential)
  - TCP pre-flight filtering (85-90% faster IP scans)
  - Smart metadata caching (4-8x faster repeat scans)

- **Adaptive Network Management (MODULE-1415):**
  - Pre-operation network quality testing
  - Dynamic delay calculation based on latency and packet loss
  - Automatic throttle adjustment during operations
  - Live visual feedback with network metrics

- **3-Pass Retry System (Universal):**
  - Certificate deployment
  - Interface configuration
  - Event management
  - Task creation
  - Backup operations
  - Silent console output (errors logged to file at DEBUG level)
  - Intelligent recovery (only retries failures)
  - ETA calculation per pass

- **Windows Performance Tuning:**
  - DefaultConnectionLimit=100 (unlocks true parallelism)
  - Expect100Continue=false (prevents EXE connection drops)
  - UseNagleAlgorithm=false (reduces latency)

- **Memory Management:**
  - Secure string bypasses for large file operations
  - Direct binary encryption for backup files (no 64KB limits)
  - Runspace disposal prevents memory leaks

---

## 📥 Download & Installation

### **Latest Release: v1.0.9**

Download the latest release from the **[Releases](../../releases/latest)** page:

- **Windows:** `ECY-Security-Manager-v1.0.9.exe` (~13 MB)
- **Linux:** `ECY-Security-Manager-v1.0.9.AppImage` (~78 MB)

**Each release includes:**
- Binary files for Windows and Linux
- SHA256 checksum files for verification
- Detailed release notes with installation instructions
- Change log and upgrade guidance

### **System Requirements**

**Windows:**
- Windows 10/11 (x64 or ARM64)
- PowerShell 5.1+ or 7.0+ (embedded in EXE)
- OpenSSL: Embedded (~10 MB, auto-extracts on first run)
- Administrator rights **ONLY** for IPv6 optimization (optional)

**Linux:**
- Most distributions (Ubuntu 20.04+, Fedora 35+, Debian 11+, Rocky Linux 8+)
- PowerShell 7.0+ (bundled in AppImage)
- OpenSSL: System package (usually pre-installed)
- No additional dependencies (fully self-contained)

### **First Run**

**Windows:**
- OpenSSL binaries extract to `%APPDATA%\EclypseManager\bin\` on first launch (~5-10 seconds)
- Subsequent runs are instant

**Linux:**
- AppImage mounts to temporary location
- Data stored in `~/.local/share/ECYSecurityManager/`
- First launch: ~5-10 seconds, subsequent: instant

**Profile Setup:**
On first launch, you'll be prompted to:
1. **Create Named Profile** (recommended) - Encrypted, persistent settings
2. **Use Temporary Profile** - No password, changes not saved

---

## 🎮 Quick Start Guide

### **1. First Launch: Profile Setup**

Create a named profile (encrypted with your password) or use temporary mode for testing.

---

### **2. Scan Your Network**

**Option 1: mDNS Discovery (Automatic)**
- Automatically discovers ECLYPSE controllers on local subnet
- Works with Avahi (Linux) or Bonjour (Windows)
- Fast: Typically finds controllers in 20-30 seconds

**Option 2: IP Range Scan**
- Validates each IP for ECLYPSE API
- Parallel scanning with TCP pre-flight filtering
- Efficient for large IP ranges

---

### **3. Generate Certificate Authority**

Follow the 8-step wizard to create a CA with full control over:
- Subject fields and constraints
- Key parameters (4096-bit recommended)
- Validity periods (10-20 years for CAs)
- Password protection (AES-256)

---

### **4. Generate Certificates**

**Quick Generate:** Uses config defaults for fast batch generation

**Custom Builder:** Full 8-step workflow with:
- Variable expansion for batch operations
- Extended key usage presets
- Subject Alternative Names (SANs)
- Template system for reuse

---

### **5. Deploy Certificates**

- Select controllers (ALL or specific)
- Choose stores (user-trusted, user-keychain, or both)
- Auto-detects format compatibility
- 3-pass retry with adaptive throttling (97-99% success rate)

---

### **6. Manage Network Interfaces**

**View Status:**
- Query all controllers for current configuration
- Shows IPv4/IPv6 states, IP addresses, operational status

**Configure Settings:**
- Select controllers and interfaces
- Choose action (enable/disable IPv4/IPv6)
- Typed confirmation for safety
- 3-pass retry with automatic verification

---

### **7. Create Scheduled Tasks (NEW in v1.0.9)**

**8-Step Workflow:**
1. Get credentials
2. Select target controllers
3. Name the task (e.g., `reboot-sunday`)
4. Build schedule using guided cron builder
5. Optional: Set expiration date
6. Configure recipients
7. Review and confirm
8. Parallel execution across all selected controllers

**Cron Builder Options:**
- Hourly: Minimum 1 hour (e.g., every 2 hours)
- Daily: Specific time (e.g., 2:00 AM)
- Weekly: Day and time (e.g., Sunday at midnight)
- Monthly: Day of month and time (e.g., 1st at 3:00 AM)
- Custom: Manual expression with validation

---

### **8. Manage Event Recipients & Tasks**

**View Recipients:**
- Query MQTT, Email, and Webhook configurations
- Parallel fetching with progress display
- Grouped by controller with details

**Delete Items:**
- Intelligent scanning across controllers
- Show item prevalence (found on X/Y controllers)
- Multi-task deletion: single (`1`), range (`1-3`), or list (`1,3,5`)
- Batch deletion with 3-pass retry
- Verification: Items not found = success

---

### **9. Schedule Automated Backups**

Create jobs for:
- Daily backup downloads
- Remote backup creation
- Age-based cleanup
- Local retention enforcement

---

## 🏗️ Architecture Overview

### **Security Architecture**

```
Profile Layer (AES-256 + PBKDF2)
  ↓
Credential Layer (3-Tier Caching)
  ↓
Certificate Layer (PKI Operations)
  ↓
Transport Layer (HTTPS API)
```

### **3-Pass Retry Flow**

```
Operation Start
  ↓
Network Quality Detection
  ↓
PASS 1: All Controllers (Silent)
  ↓
PASS 2: Retry Failures (Silent)
  ↓
PASS 3: Final Retry (Silent)
  ↓
Final Summary (Console Display)
```

---

## 🚢 Deployment Scenarios

### **Single-Site (1-20 Controllers)**
- Quick setup: ~15 minutes
- mDNS discovery
- Simple certificate generation
- Manual or scheduled backups
- **NEW:** Schedule maintenance reboots

### **Multi-Site Enterprise (100+ Controllers)**
- Template-based certificate generation
- Per-site CAs
- Automated nightly backups
- Profile export for team sharing
- Bulk interface management
- **NEW:** Centralized task automation

### **Service Provider / MSP**
- One profile per customer
- Isolated credentials and settings
- Profile export for team coordination
- Per-customer CA infrastructure
- **NEW:** Scheduled maintenance windows per site

### **IPv6 Migration**
- Bulk interface enablement
- 3-pass reliability
- Automatic verification
- Typically 97-99% success rate

### **Operations & Maintenance (NEW)**
- Scheduled controller reboots
- Time-limited automation tasks
- Bulk cleanup of expired tasks
- Event-driven workflows

---

## 🔐 Security Best Practices

- ✅ Use strong profile passwords (8+ characters)
- ✅ Export profiles periodically for backup
- ✅ Store exports in secure location
- ✅ Use named profiles for production
- ✅ Test interface changes on single controller first
- ✅ Test scheduled tasks before deploying to all controllers
- ✅ Use expiration for temporary automation
- ✅ Document baseline configurations
- ✅ Schedule during maintenance windows

---

## 📚 Advanced Features

- **Opportunistic Cache Updates:** Operations automatically update controller metadata
- **Adaptive Network Management:** Dynamic operation tuning based on real-time conditions
- **Variable Expansion:** Generate hundreds of certificates with patterns
- **Profile Export/Import:** Team sharing and disaster recovery
- **Task Expiration:** Automatic cleanup via batch API
- **Multi-Selection:** Range and list selection for bulk operations

---

## 🔧 Configuration & Tuning

### **Performance Settings**
- Max Concurrent Threads: 10-50
- Timeout: 5-60 seconds
- Operation Delay: 0-60 seconds (adaptive)
- TCP Pre-Flight: ON/OFF

### **Logging Configuration**
- File Channel: WARNING/INFO/DEBUG/TRACE
- Console Channel: ERROR/WARNING/INFO
- Per-Module Overrides
- Silent mode for retry operations

### **mDNS Discovery Settings**
- Initial/Retry Stabilization: 5-15s
- Max Retries: 0-3
- Max Threads: 1-20
- Cache Recognition: ON/OFF
- Discovery Mode: 1x Fast vs 2x Thorough

---

## 🐛 Troubleshooting

Common issues and solutions:
- OpenSSL not found
- Authentication failures during mDNS
- Slow scans
- Profile password issues
- Task creation failures
- Cron expression validation errors
- Performance optimization tips

See the detailed troubleshooting section in the full README for complete guidance.

---

## 🔄 Update System

```
Settings → Check for Updates
  → Queries GitHub Releases API
  → Compares semantic versions
  → Shows release notes preview
  → Offers one-click download with profile backup prompt
```

---

## 🌍 Localization

**Supported Languages:**
- English (en) - Default
- Français (fr) - Partial
- Deutsch (de) - Partial
- Español (es) - Partial
- Polski (pl) - Partial

**Coverage:** ~120 translation keys

---

## 📜 Legal & Licensing

### **Software License**
This software is released under the **GNU General Public License v3.0 (GPL-3.0)**.
See [LICENSE.txt](LICENSE.txt) for full terms.

### **Important Notices**
- **[DISCLAIMER.txt](DISCLAIMER.txt)** - Legal disclaimer, warranty information, and project status
- **[THIRD-PARTY-NOTICES.txt](THIRD-PARTY-NOTICES.txt)** - Third-party component licenses

### **No Telemetry**
This application:
- ✅ Collects **zero** usage data
- ✅ Makes **no** outbound connections (except manual update checks to GitHub public API)
- ✅ Stores all data locally or sends directly to your controllers
- ✅ Contains **no** tracking, analytics, or telemetry of any kind

---

## 🤝 Contributing & Support

This is a **releases-only** repository. Source code is maintained in a separate private repository.

### **Report Issues**
Use the [Issues](../../issues) tab for:
- 🐛 Bug reports
- 💡 Feature requests
- 📖 Documentation improvements

### **Community Discussions**
Use the [Discussions](../../discussions) tab for:
- ❓ General questions
- 💬 Community support
- 🎓 Tips and best practices

### **Support Availability**
Support is provided by the Distech Controls Advanced Support Team on a **discretionary basis**, primarily for:
- Distech Controls System Integrators (SI's)
- Authorized Distributors
- OEM Partners
- Other Distech Controls business partners

**Please note:** This is not covered by standard Distech Controls support agreements. Response times may vary.

---

## 📞 Contact

**Development Team:** Distech Controls Advanced Support Team
**Project Lead:** Robert Lastinger
**Purpose:** Community tool for PKI and network management in BAS environments

**For Assistance:**
- 📖 Check this [README](../../)
- 🐛 Search [Issues](../../issues)
- 💬 Ask in [Discussions](../../discussions)
- 📋 Read the [DISCLAIMER](DISCLAIMER.txt)

**For Official Distech Controls Support:**
Please contact Distech Controls through official support channels for product-related inquiries.

---

## 🏆 Acknowledgments

This tool leverages the following open-source projects:

- **[OpenSSL Project](https://www.openssl.org/)** - Certificate generation and cryptographic operations
- **[PowerShell Team](https://github.com/PowerShell/PowerShell)** - Cross-platform runtime environment
- **[PS2EXE Community](https://github.com/MScholtes/PS2EXE)** - Windows executable compilation

See [THIRD-PARTY-NOTICES.txt](THIRD-PARTY-NOTICES.txt) for complete licensing information.

---

## 📊 Project Information

**Current Version:** v1.0.9
**Versioning Scheme:** Semantic Versioning (MAJOR.MINOR.PATCH)
**Release Date:** January 12, 2026
**License:** GPL-3.0
**Status:** Community Tool - Stable Release
**Minimum PowerShell:** 7.0+
**Supported Platforms:** Windows 10/11, Linux (most distributions)

---

**Built with ⚡ by Distech Controls Advanced Support Team**

*This is a community project. Please read [DISCLAIMER.txt](DISCLAIMER.txt) before use.*

---

**📝 Version History:**
- **v1.0.9** (2026-01-12): Task Automation & Multi-Task Management
- **v1.0.8** (2026-01-08): Event Management & Scheduled Tasks
- **v1.0.7** (2026-01-07): Network Interface Management + 3-Pass Reliability
- **v1.0.1** (2026-01-06): Semantic Versioning Transition + Critical Fixes
- **v6.17.399b** (2026-01-05): UI/UX Patch (First Public)
- **v6.17.398b** (2026-01-03): Initial Public Beta