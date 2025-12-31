# Changelog

All notable changes to ECLYPSE Security Manager will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### Coming Soon
- User manual documentation
- Troubleshooting guide
- Video tutorials

---

## [6.15.351b] - 2024-12-31

### Initial Public Release

**Core Features:**
- Multi-platform support (Windows EXE, Linux AppImage)
- Certificate management (generate, deploy, delete)
- Network discovery (mDNS/Bonjour, IP range scanning)
- Backup management (create, download, restore)
- Encrypted profile system
- Multi-CA support
- Report generation (CSV, HTML)
- Job scheduling system
- Custom certificate builder with templates

**Platform Support:**
- Windows 10/11 (x64, ARM64)
- Linux distributions (Ubuntu, Fedora, Debian, etc.)
- Embedded OpenSSL for Windows
- Bundled PowerShell runtime for Linux

**Third-Party Components:**
- OpenSSL 3.5.4 (Apache License 2.0)
- PowerShell 7.x (MIT License)
- PS2EXE (MIT License)

**Known Issues:**
- None at this time

---

## Version History

This is the first public release. For earlier development history, see the private source repository.

---

**Note:** Version numbers follow the format: `MAJOR.MINOR.BUILDLETTERb`
- Example: `6.15.351b` = Major 6, Minor 15, Build 351, Beta release
