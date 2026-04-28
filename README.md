# 🛡️ Wazuh SIEM Home Lab

![Wazuh](https://img.shields.io/badge/Wazuh-SIEM-blue?style=for-the-badge&logo=wazuh)
![Platform](https://img.shields.io/badge/Platform-Windows%2011%20%7C%20Ubuntu-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)
![Blue Team](https://img.shields.io/badge/Team-Blue%20Team-blue?style=for-the-badge)

A hands-on SOC home lab built with **Wazuh SIEM**, covering real-world threat detection, file integrity monitoring, malware scanning, and automated response — designed to simulate a production SOC environment.

---

## 🖥️ Lab Architecture

| Component | Role | OS |
|-----------|------|----|
| Wazuh Manager | SIEM / Log Collector / Analyzer | Kali Linux |
| Agent 1 | Monitored Endpoint | Windows 11 |
| Agent 2 | Monitored Endpoint | Ubuntu Desktop |

---

## ✅ Implemented Modules

### 1. 📁 File Integrity Monitoring (FIM)
- Monitors critical files and directories for unauthorized changes
- Implemented on both **Windows 11** and **Ubuntu Desktop**
- Detects file creation, modification, deletion, and permission changes
- 📄 [FIM Documentation](docs/fim.md)

---

### 2. 🦠 VirusTotal Integration
- Automatically scans files flagged by FIM against **VirusTotal's** threat database
- Provides real-time threat intelligence on suspicious files
- Alerts generated on malicious file detection
- 📄 [VirusTotal Documentation](docs/virustotal.md)

---

### 3. 🔍 YARA Integration
- Uses **YARA rules** for malware pattern matching on files
- Works alongside VirusTotal for layered detection
- Custom and public YARA rulesets applied
- 📄 [YARA Documentation](docs/yara.md)

---

### 4. ⚡ Active Response
- Automated response actions triggered on security alerts
- Capable of blocking IPs, killing processes, and running custom scripts
- Configured to respond to threats detected by FIM, YARA, and VirusTotal
- 📄 [Active Response Documentation](docs/active-response.md)

---

### 5. 🔎 Vulnerability Detection
- Wazuh's built-in vulnerability detector scans agents for known CVEs
- Cross-references installed packages against NVD/CVE databases
- Provides severity scoring (CVSS) for prioritization
- 📄 [Vulnerability Detection Documentation](docs/vulnerability-detection.md)

---

## 📁 Repository Structure

```
Wazuh-SIEM-Lab/
│
├── README.md
├── configs/
│   ├── fim/
│   │   ├── windows-fim.xml
│   │   └── ubuntu-fim.xml
│   ├── virustotal/
│   │   └── virustotal-integration.xml
│   ├── yara/
│   │   └── yara-integration.xml
│   ├── active-response/
│   │   └── active-response.xml
│   └── vulnerability-detection/
│       └── vuln-detector.xml
│
├── rules/
│   └── custom-rules.xml
│
├── docs/
│   ├── fim.md
│   ├── virustotal.md
│   ├── yara.md
│   ├── active-response.md
│   └── vulnerability-detection.md
│
└── screenshots/
    └── (lab screenshots)
```

---

## 🚀 Getting Started

### Prerequisites
- Wazuh Manager installed (v4.x recommended)
- At least one Wazuh Agent connected
- VirusTotal API Key (free tier works)
- YARA installed on agent machines

### Quick Setup
1. Clone this repo
2. Copy relevant config files to your Wazuh manager (`/var/ossec/etc/`)
3. Restart Wazuh manager: `systemctl restart wazuh-manager`
4. Check alerts in Wazuh Dashboard

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| Wazuh | SIEM & XDR Platform |
| VirusTotal API | Threat Intelligence |
| YARA | Malware Pattern Matching |
| Kali Linux | Wazuh Manager Host |
| Windows 11 | Monitored Agent |
| Ubuntu Desktop | Monitored Agent |

---

## 📸 Screenshots

> Screenshots of the lab in action are available in the [`screenshots/`](screenshots/) folder.

---

## 📚 References

- [Wazuh Official Documentation](https://documentation.wazuh.com/)
- [YARA Rules Repository](https://github.com/Yara-Rules/rules)
- [VirusTotal API Docs](https://developers.virustotal.com/)
- [MITRE ATT&CK Framework](https://attack.mitre.org/)

---

## 👤 Author

**Your Name**
- 🔗 [LinkedIn](https://linkedin.com/in/yourprofile)
- 🐙 [GitHub](https://github.com/yourusername)

---

## 📜 License

This project is for educational purposes only. Use responsibly.

---

> ⭐ If you found this helpful, consider giving it a star!
