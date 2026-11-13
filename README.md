# Networkwalks-week2-footprinting-scanning
<div align="center">

# 🛡️ Week 2 — Footprinting & Network Scanning

### Cybersecurity & Ethical Hacking Internship — Networkwalks

**Muhammad Hasan Tariq** · Batch 84

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Week](https://img.shields.io/badge/Week-02-blue)
![Modules](https://img.shields.io/badge/Modules-3%2F3-success)
![Tool](https://img.shields.io/badge/OS-Kali%20Linux-557C94)
![License](https://img.shields.io/badge/Purpose-Educational-orange)

</div>

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Modules Completed](#-modules-completed)
- [📂 Repository Structure](#-repository-structure)
- [🕵️ Module 1 — GHDB Footprinting (W2-PM2)](#️-module-1--ghdb-footprinting-w2-pm2)
- [🌾 Module 2 — theHarvester OSINT (W2-PM4)](#-module-2--theharvester-osint-w2-pm4)
- [📡 Module 3 — Zenmap Network Scanning (W2-PM5)](#-module-3--zenmap-network-scanning-w2-pm5)
- [⚠️ Risk Analysis Summary](#️-risk-analysis-summary)
- [🧰 Tools & Technologies](#-tools--technologies)
- [📄 Reports](#-reports)
- [🔒 Liability Disclaimer](#-liability-disclaimer)
- [👤 Author](#-author)

---

## 📝 Overview

This repository contains my complete submission for **Week 2** of the Networkwalks Cybersecurity & Ethical Hacking Internship (**Batch 84**). Week 2 focused on the **reconnaissance / footprinting** and **scanning** phases of a penetration test:

> Reconnaissance is the first stage of every real attack. Before touching a target, an attacker (or a defender auditing themselves) quietly builds a picture of it using only public information. This week's modules put that into practice using three different tools and techniques.

All activity in this repository was conducted for **educational purposes only**, using either publicly indexed internet information or my own, self-owned local network. No private system was accessed, exploited, or modified at any point. See the [Liability Disclaimer](#-liability-disclaimer) below.

---

## ✅ Modules Completed

| # | Module | Tool | Status |
|---|---|---|:---:|
| 1 | W2-PM2 | Google Hacking Database (GHDB) | ✅ 10/10 + 10/10 |
| 2 | W2-PM4 | theHarvester | ✅ Both tasks complete |
| 3 | W2-PM5 | Zenmap (Nmap GUI) | ✅ All 7 tasks complete |
| — | W2-PM-FINAL | Combined report | ✅ Complete |

---

## 📂 Repository Structure

```
.
├── README.md                                      ← you are here
├── W2-PM-FINAL-Report-Muhammad-Hasan-Tariq.docx    ← combined report (all 3 modules)
├── W2-PM2-GHDB-Submission.docx                     ← standalone GHDB report
├── W2-PM4-theHarvester-Submission.docx             ← standalone theHarvester report
└── W2-PM5-Zenmap-Submission.docx                   ← standalone Zenmap report
```

Each `.docx` report is self-contained: background → task requirement → command/dork used → result table → evidence screenshots, in that order.

---

## 🕵️ Module 1 — GHDB Footprinting (W2-PM2)

**Tool:** [Google Hacking Database](https://www.exploit-db.com/google-hacking-database) (hosted on Exploit-DB)
**Technique:** Using pre-built Google dorks to surface sensitive, publicly indexed information without ever directly contacting the target.

### Task 1 — Live Exposed Security Cameras (10/10 ✅)

| # | Finding | Dork Used |
|---|---|---|
| 1 | Public Rome webcam (feratel.com) | `inurl:webcam site:skylinewebcams.com inurl:roma` |
| 2 | Colosseum webcam (balticlivecam.com) | `inurl:webcam site:skylinewebcams.com inurl:roma` |
| 3 | webcamXP 5, exposed pan/tilt/zoom | `intitle:"webcamXP" inurl:8080` |
| 4 | Open camera directory (153.156.0.199) | `intitle:"Index of /cam/"` |
| 5 | Ski resort webcams (lescontamines.net) | `intitle:"Index of /cam/"` |
| 6 | University of Liverpool webcam archive | `intitle:"Index of /webcam/"` |
| 7 | Open webcam directory (nihm.ca) | `intitle:"Index of /webcam/"` |
| 8 | Webcam directory leaking internal IP (ranch-turini.com) | `intitle:"Index of /webcam/"` |
| 9 | IP camera directory (quantox.co.uk) | `intitle:"Index of ipcam"` |
| 10 | Second webcamXP instance (private residence) | `intitle:"webcamxp" "Flash JPEG Stream"` |

> 📌 **Notable finding:** Finding #8 leaked an internal IP address (`192.168.1.69`) in a folder name — a real example of internal network details leaking through a misconfigured public server.

### Task 2 — Open Directories with Mathematics PDFs (10/10 ✅)

| # | Finding | Dork Used |
|---|---|---|
| 1 | erewhon.superkuh.com/library/Math/ | `intitle:index.of "parent directory" mathematics pdf` |
| 2 | ochicken.net/library/Mathematics/ | same |
| 3 | education.giakonda.org.uk/Maths/ | same |
| 4 | unm.edu/~megrad/Math/ | same |
| 5 | netlib.org/math/docpdf/ | same |
| 6 | inis.jinr.ru — Mathematics Encyclopedia PDFs | same |
| 7 | meteck.org/files/ | same |
| 8 | jsoftware.com/books/pdf | `intitle:index.of mathematics pdf` |
| 9 | math.mcgill.ca — history of mathematics texts | `intitle:index.of "parent directory" mathematics pdf` |
| 10 | download.tuxfamily.org/openmathdep/teaching/ | same |

📎 Full evidence (screenshots for every finding) is inside **`W2-PM2-GHDB-Submission.docx`**.

---

## 🌾 Module 2 — theHarvester OSINT (W2-PM4)

**Tool:** [theHarvester](https://github.com/laramies/theHarvester) (pre-installed in Kali Linux)
**Target:** `microsoft.com` (course-specified OSINT target)

### Task 1 — Baidu Source Only

```bash
theHarvester -d microsoft.com -l 1000 -b baidu
```
Result varied across runs (0–8 subdomains, 0 emails/IPs) — expected, since results depend on a live third-party source. Output saved to `pm4_task1.json` / `pm4_task1.xml`.

### Task 2 — All Sources

```bash
theHarvester -d microsoft.com -l 50 -b all
```

| Metric | Result |
|---|---|
| ASNs found | 4 (`AS13335`, `AS40034`, `AS54113`, `AS8075`) |
| IP addresses found | 134 |
| Emails found | 3 — `dotnet-docker-bot@microsoft.com`, `opencode@microsoft.com`, `secure@microsoft.com` |
| Hosts / subdomains found | 9,489 |
| Interesting URLs found | 4 |

> Several sources (BuiltWith, Censys, Shodan, etc.) returned "Missing API key" notices — expected on a clean Kali install with no API keys configured; the DNS-fallback and keyless sources still produced the large dataset above.

📎 Full command output and screenshots are inside **`W2-PM4-theHarvester-Submission.docx`**.

---

## 📡 Module 3 — Zenmap Network Scanning (W2-PM5)

**Tool:** Zenmap (Nmap GUI, pre-installed in Kali Linux)
**Target:** My own local network — `10.0.0.0/24`

| Task | Answer |
|---|---|
| 1. Zenmap installed? | ✅ Yes (pre-installed in Kali) |
| 2. Local IP & subnet | `10.0.0.2` / `10.0.0.0/24` |
| 3. Live hosts found | `10.0.0.1`, `10.0.0.2` |
| 4. Number of live hosts | 2 |
| 5. IP addresses | `10.0.0.1`, `10.0.0.2` |
| 6. MAC addresses | `10.0.0.1` → `52:54:00:12:35:00` (QEMU virtual NIC) · `10.0.0.2` → `08:00:27:a4:eb:7f` |
| 7. Topology saved as PDF? | ✅ Yes (`graph.pdf`) |

```bash
nmap -sn 10.0.0.0/24   # Zenmap profile: Ping scan
```

📎 Full evidence (ip a output, scan results, topology graph) is inside **`W2-PM5-Zenmap-Submission.docx`**.

---

## ⚠️ Risk Analysis Summary

| Risk | Impact | Level |
|---|---|:---:|
| Live, unauthenticated camera feeds (10 found) | Surveillance, situational intelligence for attackers | 🔴 High |
| Private residential camera exposed | Serious personal privacy risk to the owner | 🔴 High |
| Open directories exposing files (10 found) | Leaks internal file structure, sensitive documents | 🟠 Medium |
| Internal IP leaked via public directory | Aids further network reconnaissance | 🟠 Medium |
| Harvested public email addresses | Starting point for phishing/social engineering | 🟠 Medium |
| Large subdomain footprint (9,489 hosts) | Expands attack surface, forgotten hosts | 🟠 Medium |
| IP ranges / ASNs identified | Network/infrastructure ownership exposed | 🟡 Low |
| Local hosts visible on LAN | Unauthorized devices could go unnoticed | 🟡 Low |

Full recommendations for each risk are documented in the final report.

---

## 🧰 Tools & Technologies

![Kali Linux](https://img.shields.io/badge/Kali%20Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![Nmap](https://img.shields.io/badge/Nmap%20%2F%20Zenmap-4E9A06?style=for-the-badge&logo=nmap&logoColor=white)
![Google](https://img.shields.io/badge/Google%20Dorking-4285F4?style=for-the-badge&logo=google&logoColor=white)
![Python](https://img.shields.io/badge/theHarvester-306998?style=for-the-badge&logo=python&logoColor=white)

- **Kali Linux** — base OS for all practical work
- **Exploit-DB / GHDB** — source of Google dorks
- **Google Search** — dork execution
- **theHarvester** — OSINT / email & subdomain enumeration
- **Zenmap (Nmap GUI)** — host discovery & topology mapping

---

## 📄 Reports

| File | Contents |
|---|---|
| [`W2-PM-FINAL-Report-Muhammad-Hasan-Tariq.docx`](./W2-PM-FINAL-Report-Muhammad-Hasan-Tariq.docx) | Combined report — all 3 modules, risk analysis, recommendations, conclusion, full evidence |
| [`W2-PM2-GHDB-Submission.docx`](./W2-PM2-GHDB-Submission.docx) | GHDB — 10/10 cameras + 10/10 PDF directories with evidence |
| [`W2-PM4-theHarvester-Submission.docx`](./W2-PM4-theHarvester-Submission.docx) | theHarvester — both tasks with command output and evidence |
| [`W2-PM5-Zenmap-Submission.docx`](./W2-PM5-Zenmap-Submission.docx) | Zenmap — all 7 lab questions answered with evidence |

---

## 🔒 Liability Disclaimer

> These materials are for education and research purposes only. All footprinting activity (GHDB, theHarvester) used only publicly indexed, passive OSINT sources — no login, exploitation, or unauthorized access was attempted against any system. Network scanning (Zenmap) was performed only against my own local network, which I own and control. Hacking is only legal when you test a device/network you own, have written permission, or are operating under a signed agreement with an authorized scope. Everything outside these cases is illegal.

---

## 👤 Author

**Muhammad Hasan Tariq**
Cybersecurity & Ethical Hacking Intern — Batch 84, Networkwalks
