# ⚡ Active Response

## Overview

Active Response is a Wazuh feature that automatically executes predefined actions when specific security alerts are triggered. It enables automated threat containment without manual intervention — a key capability in real SOC environments.

---

## How It Works

1. A security alert is triggered (e.g., brute force, malware detected)
2. Wazuh matches the alert against Active Response rules
3. The defined command is executed on the target agent or manager
4. Action is logged and visible in the Wazuh Dashboard

---

## Lab Setup

| Response | Trigger | Target |
|----------|---------|--------|
| Block IP (firewall-drop) | SSH brute force (Rule 5763) | Ubuntu Agent |
| Block IP (firewall-drop) | Multiple auth failures (Rule 5712) | Ubuntu Agent |
| YARA scan | FIM file event (syscheck group) | All Agents |

---

## Commands Available

| Command | Description | OS |
|---------|-------------|-----|
| `firewall-drop` | Blocks an IP using iptables | Linux |
| `netsh.exe` | Blocks an IP using Windows Firewall | Windows |
| `restart-wazuh` | Restarts the Wazuh agent | Both |
| `yara.sh` | Runs YARA scan on a file | Linux |

---

## Location Options

| Location | Description |
|----------|-------------|
| `local` | Run on the agent that triggered the alert |
| `server` | Run on the Wazuh Manager |
| `all` | Run on all connected agents |
| `defined-agent` | Run on a specific agent by ID |

---

## Testing Active Response

```bash
# Test firewall-drop manually on Ubuntu agent
sudo /var/ossec/active-response/bin/firewall-drop add - 192.168.1.100 1234 5763

# Check if IP was blocked
sudo iptables -L | grep 192.168.1.100

# Remove the block
sudo /var/ossec/active-response/bin/firewall-drop delete - 192.168.1.100 1234 5763
```

---

## Config File

📄 [active-response.xml](../configs/active-response/active-response.xml)

---

## Screenshots

> Add your Active Response alert screenshots here from the Wazuh Dashboard.

---

## References

- [Wazuh Active Response Documentation](https://documentation.wazuh.com/current/user-manual/capabilities/active-response/index.html)
