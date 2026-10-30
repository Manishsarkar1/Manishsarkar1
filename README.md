<div align="center">

```
 ███╗   ███╗ █████╗ ███╗   ██╗██╗███████╗██╗  ██╗
 ████╗ ████║██╔══██╗████╗  ██║██║██╔════╝██║  ██║
 ██╔████╔██║███████║██╔██╗ ██║██║███████╗███████║
 ██║╚██╔╝██║██╔══██║██║╚██╗██║██║╚════██║██╔══██║
 ██║ ╚═╝ ██║██║  ██║██║ ╚████║██║███████║██║  ██║
 ╚═╝     ╚═╝╚═╝  ╚═╝╚═╝  ╚═══╝╚═╝╚══════╝╚═╝  ╚═╝
```

**Networks, packets, and the security tooling that watches them.**

Python · Scapy · raw sockets · Linux (RHCSA) · packet-level analysis

[![Status](https://img.shields.io/badge/OPEN%20TO-Security%20%2F%20Network%20Engineering%20roles-00FF88?style=for-the-badge&labelColor=0d1117)](mailto:sarkarmrigank28@gmail.com)
[![Base](https://img.shields.io/badge/BASE-Chennai%2C%20India-58A6FF?style=for-the-badge&labelColor=0d1117)](#)
[![RHCSA](https://img.shields.io/badge/CERTIFIED-RHCSA-EE0000?style=for-the-badge&logo=redhat&logoColor=white&labelColor=0d1117)](#-certifications)

**Start here → [NIDS Studio](https://github.com/Manishsarkar1/Network-Intrusion-Detection-System-NIDS-)** — a desktop IDS that captures live traffic and raises alerts on SYN scans, floods, brute-force and ARP poisoning.

</div>

---

## `$ cat profile.txt`

```bash
┌──(manish㉿kali)-[~]
└─$ cat profile.txt

  ╔═══════════════════════════════════════════════════════════╗
  ║  Name     : Manish Sarkar                                 ║
  ║  Role     : CS Undergraduate                              ║
  ║  Focus    : Network Security · Detection Engineering      ║
  ║  Base     : Chennai, India                                ║
  ║  Cert     : Red Hat Certified System Administrator        ║
  ║  Looking  : Security / Network / Backend  (intern · entry) ║
  ╚═══════════════════════════════════════════════════════════╝
```

I write low-level network code — sockets, packet capture, protocol parsing — and then build the detection logic that catches what that code can do.

My method is **build → break → defend**: I implement a technique from scratch so I know exactly what it looks like on the wire, then write the rule that flags it. The projects below are that loop, finished and running.

**Ask me about:** how the ARP-poisoning detector distinguishes a real spoof from a noisy switch, or why a SYN scanner has to be written with raw sockets to be worth anything.

---

## `$ ls -la ~/projects/ --sort=impact`

<table>
<tr>
<td width="50%" valign="top">

### 🛡️ [NIDS Studio — Network IDS](https://github.com/Manishsarkar1/Network-Intrusion-Detection-System-NIDS-)

**Problem:** a network you can't see is a network you can't defend.
**Built:** a desktop IDS — live capture on any interface, a background detection engine, and a dark GUI with a traffic rail, decoded packet view and hex dump.
**Hard part:** separating "suspicious" from "normal" without drowning the analyst — per-source alert cooldowns, tunable thresholds, and state windows per protocol.
**Result:** 6 detection classes (SYN scan, ICMP flood, UDP flood, SSH brute-force, VNC brute-force, ARP poisoning), alerts persisted to SQLite with CSV export, captures exportable to PCAP.

`Python` `Scapy` `CustomTkinter` `SQLite` · **1,900 LOC**

</td>
<td width="50%" valign="top">

### 🔍 [ScanForge — Port Scanner](https://github.com/Manishsarkar1/Port_Scanner)

**Problem:** everyone runs Nmap; almost nobody knows what it does underneath.
**Built:** a from-scratch scanning framework with no Nmap dependency — TCP connect and raw-socket SYN engines, banner grabbing and best-effort version probes.
**Hard part:** SYN scanning without the binary — hand-built packets, and a thread pool that stays fast without tripping rate limits.
**Result:** 9 protocol probes (SSH, HTTP, FTP, SMTP, POP3, IMAP, Redis, MySQL, PostgreSQL), CIDR/list parsing, JSON output, configurable workers.

`Python` `Sockets` `Scapy` `Multithreading` · **720 LOC** · ⭐ first external PR merged

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🌐 [VANTA — Moving-Target Network Defence](https://github.com/Manishsarkar1/VANTA-Variable-Network-Topology-Architecture-)

**Problem:** a static network gives an attacker unlimited time to map it.
**Built:** a Python controller that mutates topology and addressing on a schedule, an attack simulator that runs lateral-movement paths against it, and a web dashboard.
**Hard part:** making the defence measurable — a benchmark suite comparing static vs. mutated topologies instead of just asserting it works better.
**Result:** star / mesh / hybrid topology variants, benchmark reports, Apache-2.0 licensed.

`Python` `SDN` `Network Simulation` `Benchmarking` · **5,000 LOC**

</td>
<td width="50%" valign="top">

### 🖥️ [Remote GUI Framework](https://github.com/Manishsarkar1/Custom-App-only-remote-GUI-framework)

**Problem:** remote-access tools are the most abused category in security — so I built one to understand every failure mode in it.
**Built:** an application-scoped remote GUI framework (Raspberry Pi ↔ desktop) with a shared protocol layer and tests.
**Design rule:** app-level only — no OS persistence, no background service, nothing that survives the session.

`Python` `Sockets` `Architecture` · **1,150 LOC**

</td>
</tr>
</table>

---

## `$ cat /proc/skills --evidence-only`

No progress bars. Every line here links to the code that proves it.

| Skill | Where it's actually demonstrated |
|---|---|
| **Packet capture & protocol parsing** | [NIDS Studio](https://github.com/Manishsarkar1/Network-Intrusion-Detection-System-NIDS-) — live Scapy capture, TCP/UDP/ICMP/ARP decoding, hex dump |
| **Raw sockets & packet crafting** | [ScanForge](https://github.com/Manishsarkar1/Port_Scanner) — hand-built SYN probes, banner grabbing |
| **Concurrency** | [ScanForge](https://github.com/Manishsarkar1/Port_Scanner) worker pool · [NIDS](https://github.com/Manishsarkar1/Network-Intrusion-Detection-System-NIDS-) capture-thread → GUI queue |
| **Detection logic** | [NIDS `detector.py`](https://github.com/Manishsarkar1/Network-Intrusion-Detection-System-NIDS-/blob/prime/nids_core/detector.py) — thresholds, sliding windows, alert cooldowns |
| **SQL / storage** | SQLite alert store (NIDS) · MySQL schema + queries ([LMS](https://github.com/Manishsarkar1/Learning-Mangement-System)) |
| **Linux & systems** | RHCSA — filesystem, users, systemd, SELinux, networking, no multiple-choice |
| **Desktop & web UI** | CustomTkinter (NIDS) · Express + JWT + bcrypt (LMS) · web dashboard (VANTA) |
| **Python · Bash · JavaScript** | ~8,900 lines of Python across 4 repos; shell entry points in VANTA; Node/Express in LMS |

**Working rules I keep:** every security repo documents the privileges it needs (root / Npcap) and carries a legal-use note; all testing happens in isolated VMs on networks I own; tooling is built from source, not wrapped around an existing binary.

---

## 🏅 Certifications

<div align="center">

| Certification | Issuer | Covers |
|---|---|---|
| 🎖️ **Red Hat Certified System Administrator (RHCSA)** | Red Hat, Inc. | Filesystem · users & permissions · systemd · SELinux · networking · containers — 100% hands-on exam |

</div>

> Red Hat publishes a verification endpoint for every credential holder. If you need the verification ID for a background check, ask and I'll send it — it resolves against Red Hat's records, not mine.

---

## `$ tail -f /var/log/security_lab.log`

```log
[DONE]  NIDS Studio — 6 detection classes, SQLite alert store, CSV + PCAP export
[DONE]  ScanForge  — connect + SYN engines, 9 protocol probes, JSON output, external PR merged
[DONE]  VANTA      — topology mutation under attack simulation, benchmark suite, Apache-2.0
[DONE]  RHCSA      — Linux administration under exam conditions
[NOW]   Test coverage + CI for NIDS and ScanForge (pytest + GitHub Actions)
[NOW]   Exploit-development fundamentals — buffer overflows in a lab-only VM
[NEXT]  Three technical writeups — one per project, published, with real packet captures
[NEXT]  v1.0 tagged release for NIDS, with a test suite that runs on every push
```

---

## `$ cat roadmap.yml`

```yaml
current_focus:
  - Detection engineering: thresholds, false-positive control, alert design
  - Packet-level protocol analysis (TCP/UDP/ICMP/ARP)
  - Test coverage and CI on every project I ship
  - Exploit development fundamentals — buffer overflows, lab-only

certifications:
  completed:
    - RHCSA (Red Hat Certified System Administrator)
  next:
    - CompTIA Security+  # or eJPT, whichever fits the role I land

next_90_days:
  - NIDS v1.0: pytest suite + GitHub Actions CI + tagged release
  - Publish 3 writeups with packet captures and benchmark numbers
  - One merged pull request in an upstream open-source security project
  - Purge every secret and build artifact from history, then re-scan with gitleaks

philosophy: "offensive understanding → defensive engineering"
```

---

## `$ git log --all --graph --oneline`

<div align="center">

![GitHub Stats](https://github-readme-stats-sigma-five.vercel.app/api?username=Manishsarkar1&hide_border=true&title_color=00FF88&text_color=c9d1d9&bg_color=0d1117&show_icons=true&icon_color=00FF88)
&nbsp;&nbsp;
![Top Languages](https://github-readme-stats-sigma-five.vercel.app/api/top-langs/?username=Manishsarkar1&hide_border=true&title_color=00FF88&text_color=c9d1d9&bg_color=0d1117&layout=compact&langs_count=6&card_width=300)

![Contribution activity](https://raw.githubusercontent.com/Manishsarkar1/Manishsarkar1/output/github-contribution-grid-snake-dark-static.svg)

</div>

---

## `$ netstat --established`

<div align="center">

[![Email](https://img.shields.io/badge/Email-sarkarmrigank28%40gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white&labelColor=0d1117)](mailto:sarkarmrigank28@gmail.com)
&nbsp;
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Manish%20Sarkar-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white&labelColor=0d1117)](https://www.linkedin.com/in/manishsarkar/)
&nbsp;
[![GitHub](https://img.shields.io/badge/GitHub-Manishsarkar1-ffffff?style=for-the-badge&logo=github&logoColor=white&labelColor=0d1117)](https://github.com/Manishsarkar1)

*Chennai, India · open to on-site, hybrid and remote · reply within a day*

</div>

---

<div align="center">

```
┌─────────────────────────────────────────────────────────────────────┐
│   All security research is conducted in isolated, air-gapped        │
│   virtual environments strictly for educational purposes.           │
│   Knowledge is a tool — intent is everything.                       │
└─────────────────────────────────────────────────────────────────────┘
```

![Footer](https://capsule-render.vercel.app/api?type=waving&color=00FF88&height=80&section=footer)

</div>
