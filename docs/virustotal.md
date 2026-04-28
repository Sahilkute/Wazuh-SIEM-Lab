# 🦠 VirusTotal Integration

## Overview

VirusTotal is a free online threat intelligence service that analyzes files and URLs using 70+ antivirus engines. Wazuh integrates with VirusTotal to automatically scan files flagged by FIM against its database.

---

## How It Works

1. FIM detects a new or modified file on an agent
2. Wazuh extracts the file hash (MD5/SHA256)
3. The hash is sent to VirusTotal API
4. VirusTotal returns a scan report
5. If flagged as malicious → Wazuh generates a high-priority alert

---

## Lab Setup

| Component | Details |
|-----------|---------|
| API Type | VirusTotal Free API |
| Trigger | FIM file events (syscheck group) |
| Agents Monitored | Windows 11 + Ubuntu Desktop |

---

## Alert Rules

| Rule ID | Description | Level |
|---------|-------------|-------|
| 87101 | VirusTotal query performed | 3 |
| 87102 | File not found in VirusTotal | 3 |
| 87103 | File found, 0 engines flagged | 5 |
| 87104 | File found, at least 1 engine flagged | 8 |
| 87105 | File found, multiple engines flagged | 12 |

---

## Setup Steps

1. Sign up for a free API key at [virustotal.com](https://www.virustotal.com)
2. Add integration config to Wazuh Manager `ossec.conf`
3. Replace `YOUR_VIRUSTOTAL_API_KEY_HERE` with your actual key
4. Restart Wazuh Manager:
```bash
systemctl restart wazuh-manager
```
5. Test by dropping a known malicious hash file on a monitored agent

---

## Config File

📄 [virustotal-integration.xml](../configs/virustotal/virustotal-integration.xml)

---

## Screenshots

> Add your VirusTotal alert screenshots here from the Wazuh Dashboard.

---

## References

- [Wazuh VirusTotal Integration Guide](https://documentation.wazuh.com/current/user-manual/capabilities/malware-detection/virus-total-integration.html)
- [VirusTotal API Documentation](https://developers.virustotal.com/)
