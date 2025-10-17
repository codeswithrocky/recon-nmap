# recon-nmap

**Automated Nmap Scan & Report Generator**  
Runs `nmap`, saves raw outputs, parses the XML to JSON, and produces a human-friendly HTML report.

**Version:** 0.1.0  
**Author:** Rocky

---

## ⚙️ What it does

`recon-nmap` automates a typical Nmap workflow and saves multiple outputs:

- `<prefix>.xml` — raw Nmap XML (used for parsing)
- `<prefix>.nmap` — normal Nmap output
- `<prefix>.gnmap` — grepable Nmap output
- `<prefix>.summary.json` — parsed JSON summary extracted from XML
- `<prefix>.report.html` — readable HTML report (open in any browser)

The tool ships as a single-file Python CLI named `recon-nmap`. A man page `recon-nmap.1` is included.

> **Important:** This script calls the `nmap` binary. Install Nmap and run only against hosts/networks you have permission to scan.

---

## 🔧 Requirements

- Python 3.8+
- `nmap` CLI installed and in your `PATH`
- (Optional) `help2man` if you want to auto-generate man pages in other formats

---

## 📥 Installation (quick)

Copy and make executable (example):
```bash
# from repo root
chmod +x recon-nmap
sudo mv recon-nmap /usr/local/bin/recon-nmap
