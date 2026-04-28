# 📁 File Integrity Monitoring (FIM)

## Overview

File Integrity Monitoring (FIM) is a security technique that monitors files and directories for unauthorized changes. Wazuh's FIM module detects file creation, modification, deletion, and permission changes in real time.

---

## Lab Setup

| Agent | OS | Monitoring Mode |
|-------|-----|----------------|
| Agent 1 | Windows 11 | Real-time |
| Agent 2 | Ubuntu Desktop | Real-time + Whodata |

---

## How It Works

1. Wazuh agent scans monitored directories and creates a baseline database of file hashes
2. Any change to a monitored file triggers an alert
3. The alert includes: file path, old hash, new hash, who changed it (Whodata), and timestamp
4. Alerts are visible in the Wazuh Dashboard under **File Integrity Monitoring**

---

## Monitored Paths

### Windows 11
| Path | Reason |
|------|--------|
| `C:\Users` | User profile changes |
| `C:\Windows\System32` | Critical system files |
| `C:\Program Files` | Installed software |
| Registry: `HKLM\...\Run` | Persistence detection |

### Ubuntu Desktop
| Path | Reason |
|------|--------|
| `/etc` | System configuration |
| `/usr/bin` | Executable binaries |
| `/home` | User files |
| `/root` | Root user files |
| `/tmp` | Temp file abuse detection |

---

## Alert Levels

| Rule ID | Description | Level |
|---------|-------------|-------|
| 550 | File modified | 7 |
| 553 | File deleted | 7 |
| 554 | New file created | 5 |
| 556 | File ownership changed | 8 |

---

## Config File

📄 [windows-fim.xml](../configs/fim/windows-fim.xml)
📄 [ubuntu-fim.xml](../configs/fim/ubuntu-fim.xml)

---

## Screenshots

> Add your FIM alert screenshots here from the Wazuh Dashboard.

---

## References

- [Wazuh FIM Documentation](https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/index.html)
