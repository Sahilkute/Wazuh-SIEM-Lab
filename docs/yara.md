# 🔍 YARA Integration

## Overview

YARA is a tool used to identify and classify malware based on pattern matching rules. Each YARA rule defines patterns (strings, byte sequences, conditions) that match known malware families. Wazuh integrates YARA via Active Response to scan files detected by FIM.

---

## How It Works

1. FIM detects a new or modified file
2. Active Response triggers `yara.sh` script on the agent
3. YARA scans the file against all loaded rules
4. If a rule matches → Wazuh generates a malware detection alert

---

## Lab Setup

| Component | Details |
|-----------|---------|
| YARA Version | Latest stable |
| Rules Used | Public YARA-Rules repo + custom rules |
| Trigger | FIM syscheck events via Active Response |
| Agents | Windows 11 + Ubuntu Desktop |

---

## Alert Rules

| Rule ID | Description | Level |
|---------|-------------|-------|
| 108501 | YARA scan triggered | 3 |
| 108502 | YARA rule matched — malware detected | 12 |

---

## Setup Steps

### On Ubuntu Agent
```bash
# Install YARA
sudo apt-get install yara -y

# Create rules directory
sudo mkdir -p /tmp/yara/rules

# Download public YARA rules
cd /tmp/yara/rules
sudo wget https://github.com/Yara-Rules/rules/archive/refs/heads/master.zip
sudo unzip master.zip

# Copy YARA active response script
sudo cp yara.sh /var/ossec/active-response/bin/
sudo chmod 750 /var/ossec/active-response/bin/yara.sh
sudo chown root:wazuh /var/ossec/active-response/bin/yara.sh
```

### On Windows Agent
```powershell
# Download YARA for Windows from https://github.com/VirusTotal/yara/releases
# Place yara64.exe in:
# C:\Program Files (x86)\ossec-agent\active-response\bin\

# Create rules folder:
# C:\Program Files (x86)\ossec-agent\active-response\bin\yara\rules\
```

---

## Config File

📄 [yara-integration.xml](../configs/yara/yara-integration.xml)

---

## Screenshots

> Add your YARA alert screenshots here from the Wazuh Dashboard.

---

## References

- [Wazuh YARA Integration Guide](https://documentation.wazuh.com/current/proof-of-concept-guide/detect-malware-yara-integration.html)
- [YARA Rules Repository](https://github.com/Yara-Rules/rules)
- [YARA Official Documentation](https://yara.readthedocs.io/)
