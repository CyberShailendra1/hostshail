# 🛡️ hostshail — Host Header Vulnerability Scanner

```
  ██╗  ██╗ ██████╗ ███████╗████████╗███████╗██╗  ██╗ █████╗ ██╗██╗
  ██║  ██║██╔═══██╗██╔════╝╚══██╔══╝██╔════╝██║  ██║██╔══██╗██║██║
  ███████║██║   ██║███████╗   ██║   ███████╗███████║███████║██║██║
  ██╔══██║██║   ██║╚════██║   ██║   ╚════██║██╔══██║██╔══██║██║██║
  ██║  ██║╚██████╔╝███████║   ██║   ███████║██║  ██║██║  ██║██║███████╗
  ╚═╝  ╚═╝ ╚═════╝ ╚══════╝   ╚═╝   ╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝╚═╝╚══════╝
```

> **Host Header Vulnerability Scanner for penetration testers and security researchers.**  
> Author: **CyberShailendra** | Version: `1.0.0` | Platform: Kali Linux

---

## 📋 Table of Contents
- [Features](#-features)
- [Checks Performed](#-checks-performed)
- [Installation](#-installation)
- [Usage](#-usage)
- [Examples](#-examples)
- [Output / Reporting](#-output--reporting)
- [Disclaimer](#-disclaimer)

---

## ✨ Features

- ✅ **11 distinct vulnerability checks** in a single run
- ✅ Colored, severity-tagged terminal output (CRITICAL / HIGH / MEDIUM / LOW / INFO)
- ✅ Multi-target scanning with threading support
- ✅ JSON and plain-text report export
- ✅ Proxy support (Burp Suite / ZAP integration)
- ✅ Custom User-Agent and timeout control
- ✅ Zero external binary dependencies — pure Python

---

## 🔍 Checks Performed

| # | Check | Severity |
|---|-------|----------|
| 1 | Basic Host Header Injection (reflection) | HIGH |
| 2 | Password Reset Link Poisoning | CRITICAL |
| 3 | Web Cache Poisoning via Host Header | CRITICAL / MEDIUM |
| 4 | Open Redirect via Host Header | HIGH |
| 5 | SSRF via Host Header (cloud metadata) | CRITICAL |
| 6 | Absolute URL Injection in Request-Line | HIGH |
| 7 | HTTP Request Smuggling Indicators | MEDIUM |
| 8 | Access Control Bypass (localhost spoof) | HIGH |
| 9 | Conflicting / Duplicate Host Headers | MEDIUM |
| 10 | SNI vs Host Header Mismatch (HTTPS) | LOW |
| 11 | Response Fingerprinting | INFO |

---

## 🔧 Installation

### Requirements
- Python 3.8+
- Kali Linux (or any Linux distro)

### Quick Install

```bash
git clone https://github.com/CyberShailendra1/hostshail.git
cd hostshail
pip3 install -r requirements.txt
chmod +x hostshail.py
```

### One-liner (Kali)

```bash
git clone https://github.com/CyberShailendra1/hostshail.git && cd hostshail && pip3 install -r requirements.txt
```

---

## 🚀 Usage

```
usage: hostshail [-h] [-u URL] [-l LIST] [-o OUTPUT] [-v] [-t THREADS]
                 [--timeout TIMEOUT] [--proxy PROXY] [--ua UA] [--version]

Host Header Vulnerability Scanner | Author: CyberShailendra

options:
  -h, --help            show this help message and exit
  -u URL, --url URL     Single target URL
  -l LIST, --list LIST  File with target URLs (one per line)
  -o OUTPUT, --output OUTPUT
                        Output file (report.json or report.txt)
  -v, --verbose         Verbose output
  -t THREADS, --threads THREADS
                        Threads for multi-target scanning (default: 5)
  --timeout TIMEOUT     Request timeout in seconds (default: 10)
  --proxy PROXY         Proxy URL  e.g. http://127.0.0.1:8080
  --ua UA               Custom User-Agent string
  --version             show program's version number and exit
```

---

## 📌 Examples

**Scan a single target:**
```bash
python3 hostshail.py -u https://target.com
```

**Verbose mode (show all probes):**
```bash
python3 hostshail.py -u https://target.com -v
```

**Scan a list of targets with 10 threads:**
```bash
python3 hostshail.py -l targets.txt -t 10
```

**Save results as JSON:**
```bash
python3 hostshail.py -u https://target.com -o report.json
```

**Save results as plain text:**
```bash
python3 hostshail.py -u https://target.com -o report.txt
```

**Route through Burp Suite:**
```bash
python3 hostshail.py -u https://target.com --proxy http://127.0.0.1:8080
```

**Custom User-Agent:**
```bash
python3 hostshail.py -u https://target.com --ua "Mozilla/5.0 (custom)"
```

---

## 📊 Output / Reporting

Terminal output is color-coded:

| Color | Severity |
|-------|----------|
| 🔴 Red (CRITICAL) | Immediate risk — e.g., confirmed cache poisoning, reset poisoning |
| 🔴 Red (HIGH) | Exploitable injection or bypass |
| 🟡 Yellow (MEDIUM) | Requires further manual verification |
| 🔵 Cyan (LOW) | Low-risk informational finding |
| 🔵 Blue (INFO) | Server fingerprint / metadata |

JSON report structure:
```json
{
  "target": "https://target.com",
  "timestamp": "2025-01-01T12:00:00",
  "summary": {
    "total": 3,
    "critical": 1,
    "high": 2,
    "medium": 0,
    "low": 0,
    "info": 0
  },
  "vulnerabilities": [
    {
      "check": "basic_injection",
      "severity": "HIGH",
      "title": "Host Header Injection via 'X-Forwarded-Host'",
      "detail": "Injected value reflected in response.",
      "evidence": { "Header": "X-Forwarded-Host", "Payload": "evil.attacker.com" }
    }
  ]
}
```

---

## 🛡️ Severity Guide

| Severity | Description |
|----------|-------------|
| **CRITICAL** | Direct impact — password reset poisoning, cache poisoning, SSRF to metadata |
| **HIGH** | Injected data reflected, open redirects, access control bypass |
| **MEDIUM** | Potential vectors requiring manual confirmation |
| **LOW** | Informational / configuration weaknesses |
| **INFO** | Server technology fingerprint |

---

## ⚠️ Disclaimer

> **hostshail** is intended for **authorized security testing and educational purposes only**.  
> Use only on systems you own or have explicit written permission to test.  
> The author, **CyberShailendra**, holds no responsibility for misuse or illegal activity.  
> Always comply with applicable laws and your organization's security policies.

---

## 📄 License

MIT License — see [LICENSE](LICENSE)

---

## 👤 Author

**CyberShailendra**  
GitHub: [@CyberShailendra](https://github.com/CyberShailendra1)

---

*If this tool helped you, consider giving it a ⭐ on GitHub!*
