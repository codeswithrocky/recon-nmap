# recon-nmap

**Automated Nmap Scan & Report Generator**  
Runs `nmap`, saves raw outputs, parses the XML to JSON, and produces a human-friendly HTML report.

**Version:** 0.1.0  
**Author:** Rocky

---

## What it does

`recon-nmap` automates a typical Nmap workflow and saves multiple outputs:

- `<prefix>.xml` — raw Nmap XML (used for parsing)  
- `<prefix>.nmap` — normal Nmap output  
- `<prefix>.gnmap` — grepable Nmap output  
- `<prefix>.summary.json` — parsed JSON summary extracted from XML  
- `<prefix>.report.html` — readable HTML report (open in any browser)

Ships as a single-file Python CLI `recon-nmap`. A man page `recon-nmap.1` is included.

> Important: Only scan hosts/networks you have explicit permission to test. Unauthorized scanning can be illegal.

---

## Requirements

- Python 3.8+  
- `nmap` CLI installed and in your PATH  
- (Optional) `help2man` if you want to auto-generate or update manpages

---

## Installation

### 1) Install script
```bash
chmod +x recon-nmap
sudo mv recon-nmap /usr/local/bin/recon-nmap
```

### 2) Install manpage (optional)

**Linux (Debian/Ubuntu)**
```bash
sudo cp recon-nmap.1 /usr/local/share/man/man1/
sudo mandb
man recon-nmap
```

**macOS**
```bash
sudo cp recon-nmap.1 /usr/local/share/man/man1/
man -M /usr/local/share/man recon-nmap
```

### 3) Uninstall
```bash
sudo rm /usr/local/bin/recon-nmap
sudo rm /usr/local/share/man/man1/recon-nmap.1
sudo mandb   # optional (Debian/Ubuntu)
```





## Usage

Basic single target:

```bash
recon-nmap -t example.com -o ./reports/example
```

Multiple targets:

```bash
recon-nmap -t 10.0.0.1 10.0.0.0/24 example.com -o ./reports/batch
```

Targets from file:

```bash
recon-nmap -iL targets.txt -o ./reports/batch1
```

Preset profiles:

```bash
recon-nmap -t example.com -p default
recon-nmap -t example.com -p quick
recon-nmap -t example.com -p stealth
recon-nmap -t example.com -p full
```

Append raw nmap arguments:

```bash
recon-nmap -t example.com --extra -p 80,443 -sS
```

Parse existing XML without running nmap:

```bash
recon-nmap --no-run -o ./reports/example
```

Help & version:

```bash
recon-nmap --help
recon-nmap --version
```

---

## Output

Example `--outdir ./reports/example` with default prefix `scan`:

```
./reports/example/scan.xml
./reports/example/scan.nmap
./reports/example/scan.gnmap
./reports/example/scan.summary.json
./reports/example/scan.report.html
```

Open `scan.report.html` in a browser.

---

## How it works

1. Builds an `nmap` command with chosen profile and extra arguments.
2. Runs `nmap` and generates `.xml`, `.nmap`, `.gnmap`.
3. Parses XML to extract hosts, addresses, ports, services, scripts, OS matches.
4. Creates `.summary.json` and a styled `.report.html`.

---

## Ethics & Legal

Scan only systems you own or have explicit authorization for. Unauthorized scanning is illegal.

---

## Testing

Add smoke tests (example: `tests/smoke_test.sh`):

```bash
#!/usr/bin/env bash
set -e
recon-nmap --version
recon-nmap --help | head -n 5
echo "smoke ok"
```

Make executable:

```bash
chmod +x tests/smoke_test.sh
```

---

## Troubleshooting

* **nmap not found** → Ensure `nmap` installed and in PATH
* **XML parse errors** → Ensure `.xml` file exists and was fully written by nmap
* **Scan too slow/noisy** → Use `-p quick` or `-p stealth`, or smaller port set
* **Permission denied saving files** → Ensure `--outdir` is writable

---

## Contact / Security

Bugs or security concerns: `support@codelivly.com`

---

