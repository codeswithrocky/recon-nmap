Perfect — I understand! You want a **single `README.md`** that contains **everything in one place**, including:

* Description
* Requirements
* Installation (script + manpage)
* Usage
* Outputs
* Troubleshooting
* Contribution
* CI/GitHub guide
* License
* Contact

Here’s a fully consolidated `README.md` ready to drop into your repo:

````markdown
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

Ships as a single-file Python CLI `recon-nmap`. A man page `recon-nmap.1` is included.

> **Important:** Only scan hosts/networks you have explicit permission to test. Unauthorized scanning can be illegal.

---

## 🔧 Requirements

- Python 3.8+  
- `nmap` CLI installed and in your PATH  
- (Optional) `help2man` if you want to auto-generate or update manpages

---

## 📥 Installation

### 1) Install script
```bash
chmod +x recon-nmap
sudo mv recon-nmap /usr/local/bin/recon-nmap
````

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

---

## 🧭 Usage

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

## 🗂 Output

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

## 🛠 How it works

1. Builds an `nmap` command with chosen profile and extra arguments.
2. Runs `nmap` and generates `.xml`, `.nmap`, `.gnmap`.
3. Parses XML to extract hosts, addresses, ports, services, scripts, OS matches.
4. Creates `.summary.json` and a styled `.report.html`.

---

## ⚖️ Ethics & Legal

Scan only systems you own or have explicit authorization for. Unauthorized scanning is illegal.

---

## 🧪 Testing

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

## 🛟 Troubleshooting

* **nmap not found** → Ensure `nmap` installed and in PATH
* **XML parse errors** → Ensure `.xml` file exists and was fully written by nmap
* **Scan too slow/noisy** → Use `-p quick` or `-p stealth`, or smaller port set
* **Permission denied saving files** → Ensure `--outdir` is writable

---

## 🧩 Contributing

1. Fork repo
2. Create branch: `git checkout -b feature/<name>`
3. Add changes/tests
4. Commit with descriptive message
5. Open a Pull Request with summary and testing steps

Coding style: Python 3.8+, follow PEP8. Optional: use `black`.

---

## 🔁 CI / GitHub Actions

Minimal workflow: lint & run smoke tests in `.github/workflows/ci.yml`.

---

## 📦 Packaging (optional)

* Move CLI into Python module
* Add `setup.cfg`/`pyproject.toml`
* Create entry point for pip install
* Add tests & optionally publish to PyPI

---

## 🧾 License

MIT License — see `LICENSE`.

---

## 📤 GitHub setup & push

**Option A — GitHub web UI**

1. Create repo
2. Local commands:

```bash
git init
git add .
git commit -m "Initial commit — recon-nmap v0.1.0"
git branch -M main
git remote add origin git@github.com:YOUR_USERNAME/recon-nmap.git
git push -u origin main
```

**Option B — GitHub CLI**

```bash
git init
git add .
git commit -m "Initial commit"
gh repo create YOUR_USERNAME/recon-nmap --public --source=. --remote=origin --push
```

**Tag & release**

```bash
git tag -a v0.1.0 -m "v0.1.0"
git push origin v0.1.0
gh release create v0.1.0 --title "v0.1.0" --notes "Initial release"
```

---

## 📬 Contact / Security

Bugs or security concerns: `support@codelivly.com` (replace with your contact). Prefer private disclosure before public.

---

Thanks — enjoy `recon-nmap`!

```

This single `README.md` now **contains every instruction, manpage info, installation, usage, troubleshooting, CI, contribution, license, and GitHub guidance** — everything in one page.

If you want, I can **also add a small section inside it that directly shows example HTML report screenshots** and file structure, so your users immediately know what to expect visually.  

Do you want me to add that?
```
