# GitHub Audit — Manish Sarkar (`Manishsarkar1`)

**Reviewed as:** technical recruiter + hiring manager for entry-level Security Engineer / Network Engineer / SOC Analyst roles in India.
**Method:** read your profile, all 9 public repos, commit history, PRs, branches, and file trees. Nothing here is a guess — every claim below has a file, commit or URL behind it.
**Date:** 30 Oct 2026

---

## Verdict in one paragraph

Your **work is above average for a student. Your packaging is below average for a professional.** That gap is the entire reason you're not getting calls. The code says "this person actually builds packet-level tooling." The profile around it says "hobbyist who dumps projects on weekends" — vague claims, no tests, no CI, no writing, no third-party validation, and one committed `.env` file that would end the conversation in 30 seconds if a security lead saw it. Fixable in about two weeks of evenings. Ranked by damage below.

## Scorecard

| Dimension | Score | One-line reason |
|---|---|---|
| Technical substance | **7.5 / 10** | Real Scapy/socket code, 1,900-LOC IDS with 6 detection classes — genuinely above student average |
| Code quality & structure | **6 / 10** | Sensible module layout (`nids_core/`, `scanner_framework/`) — but `__pycache__` and 67 MB repos committed |
| Repo hygiene | **3 / 10** | Committed `.env` with secrets, `node_modules/`, a 700 KB `.pkl`, an empty repo, no `.gitignore` on 6 of 7 |
| Commit discipline | **3 / 10** | `made things`, `something++`, `NULL`, one empty message, 15 commits in a single day |
| Test & CI maturity | **2 / 10** | 0 test files in 6 of 7 repos, 0 CI workflows, 0 releases, 0 tags |
| Third-party validation | **1 / 10** | 0 external PRs, 0 issues filed, 1 star, 6 followers — nobody has ever reviewed your code |
| Presentation / discoverability | **4 / 10** | Beautiful README, wrong information hierarchy; 5 of 9 repos have no description, 7 of 9 no topics |
| Honesty of claims | **4 / 10** | C "████████", Metasploit, Burp Suite, "CTF competitions" — none of it has an artifact behind it |
| **Would I shortlist today?** | **No** | **Would I shortlist after the 2-week fix list? Yes — probably interview.** |

---

## The 10 things costing you the interview, ranked by damage

### 1. You committed `.env` with live-looking secrets to a public repo 🔴 *disqualifying*

`Learning-Mangement-System/.env` is public and contains `JWT_SECRET`, `DB_PASSWORD`, `DB_USER`, `DB_NAME`. Same repo also has `node_modules/`, `.npm-cache/` and a generated `README.html` committed — 10.4 MB for a student CRUD app.

You are applying as a **security** candidate. The single fastest way to fail a security interview is to hand the interviewer a public repo with a JWT signing key in it. This is not a style issue, it's the exact failure class the job exists to prevent. An interviewer who finds this stops reading and starts writing "does not understand secrets management" on the scorecard.

**Fix (today):** rotate the values, `git rm --cached .env`, add `.gitignore`, then rewrite history with `git filter-repo` or BFG — deleting the file in a new commit is **not** enough, it stays in history forever. Then run `gitleaks detect` across all 9 repos and fix everything it finds.

### 2. Your profile makes claims your repos can't defend 🔴 *integrity flag*

I checked every skill claim on the old README against your code:

| Old claim | Reality |
|---|---|
| `C ████████░░░░ systems` | **Zero C files in any of your 9 repos.** Not one. |
| `Metasploit → Exploitation` | No artifact, no writeup, no tooling |
| `Burp Suite → Web Attack Surface` | No artifact, no writeup |
| NIDS "**built entirely from scratch**" | Your own repo description says *"Just a jump start to packet sniffing and manipulation"* — a recruiter who opens the repo sees the contradiction immediately |
| `[NEXT] → CTF competitions · CVE research · Bug bounty` | User-confirmed: you have no CTFs and no hackathon wins |

The last one is the one that hurts. Recruiters are trained to hunt for the one inflated line that lets them junk a profile. You gave them six. **A profile with 5 claims and 5 proofs beats a profile with 15 claims and 5 proofs — every single time, in every company.** Your old README scored 15/5.

### 3. Nothing on your profile has been validated by another human 🔴

Hard numbers from the GitHub API:

- **4 pull requests authored, 3 merged — all 4 are your own branches into your own repos.** (Two into `Manishsarkar1`, one into `Port_Scanner`, one closed unmerged.)
- **0 issues ever filed** on anyone's repo.
- **0 commits to any repository you don't own.**
- **1 star, 6 followers, 1 contributor** to your projects (a first-timer adding a clone step to your README).

So: no code review, no collaboration, no upstream contribution, no community. For an entry-level hire this is *normal*, but you have zero compensating evidence — which means the hiring manager has to take your word for everything. They won't.

### 4. Zero tests. Zero CI. Zero releases. Nothing you've built is "done" 🟠

- `Port_Scanner`: 0 tests. `NIDS`: 0 tests. `Custom GUI`: has a `tests/` folder — the only one. `VANTA`: has `tests/`, good.
- `.github/workflows/` exists in **one** repo: your profile repo, and it only generates a snake animation.
- **0 releases, 0 tags** across all repos.

For a security role, "does it have a test?" is the question that separates a script from a product. Six detection rules with no tests means you cannot tell me your ARP-poisoning detector works — you can only tell me it ran once.

Worse: that one workflow generates a snake SVG into your `output` branch, and your README **never referenced the image**. You had working automation whose output nobody could see. That's the most on-brand summary of this whole audit — and I've now wired it into the README.

### 5. Your commit history reads like a diary, not an engineering log 🟠

Actual messages from your repos:

```
made things                    ← HPC-project, the entire second commit
made changes                   ← VANTA
changes ++                     ← VANTA
something++                    ← UPI-vanguard
good good changes              ← UPI-vanguard
NULL                           ← Learning-Mangement-System (message literally "NULL")
(empty message)                ← UPI-vanguard
made the UI cooler             ← Remote GUI Framework
made it roll back to research based
```

Plus the timing problem: **NIDS got its entire core — 15 commits — on 2026-03-07 in one day.** LMS got ~14 commits on 2026-03-26/27. When a hiring manager sees a 1,900-line IDS built in a single afternoon, the first hypothesis is not "prolific" — it's "generated" or "copied." You undo the credibility of genuinely good work with the metadata around it.

### 6. Repo hygiene that signals a beginner 🟠

| Repo | Problem |
|---|---|
| `HPC-project` | **67 MB** — `dist/` and `data/` committed, no `.gitignore`, second commit is "made things" |
| `VANTA` | `__pycache__/` committed, no `.gitignore`, 4.2 MB |
| `distributed_graph_processing_unit` | **Completely empty** — a 35-byte README and nothing else, default branch `prime`. A dead repo on a 9-repo profile is 11% of your portfolio being a hole |
| `UPI-vanguard` | No description, README says only *"basic structure"*, and a **710 KB `Fraud_model.pkl`** committed instead of released |
| `Learning-Mangement-System` | Misspelled name ("Mangement"), `.env` + `node_modules/`, no description |
| Branch names | Default branches are `prime`, `prime`, `prime`, `Prototype2`, `master`, `master` — meaning you've never used a PR into a protected branch on your own projects. Also leftover `CL` and `Testing` branches |

### 7. Six of nine repos are invisible in search 🟡

- **5 of 9 have no description** (HPC-project, distributed_graph, LMS, Custom GUI, UPI-vanguard).
- **7 of 9 have no topics.**
- **Only 2 of 9 have a license** (MIT on NIDS, Apache-2.0 on VANTA). No license = legally, nobody can use or reuse your code. For a security tool that's a real defect.

A recruiter searching GitHub for `python ids scapy` will never find you. Descriptive text and topics are the cheapest SEO you will ever get.

### 8. You're missing every filter an HR screen actually uses 🟡

Your profile right now:

- **Location: "Milky way."** Recruiters filter by city. Chennai openings filter to Chennai. You are unlisted.
- **Bio:** `if it runs on a network, i'm either scanning it or defending it.` — charming, tells me nothing about what you want.
- **No role target, no availability, no graduation year, no résumé link.**
- **HackTheBox badge links to `academy.hackthebox.com/app/dashboard`** — a *logged-in dashboard*, not a public profile. Every recruiter who clicks it lands on a login wall. Dead link.
- **TryHackMe badge** to a profile with no visible proof of activity.
- **No screenshots anywhere.** You built a dark-themed GUI with a packet inspector and hex dump — and there is not one image of it on your profile. **A GUI tool with no screenshot is a claim without evidence.** Screenshots convert; they're the cheapest credibility on the internet.

### 9. Zero writing 🟡

No blog, no writeups, no dev.to, no Medium, no `docs/` with findings. In security hiring, writing is *the* differentiator, because a writeup proves you understood a thing rather than installed a thing. Your VANTA repo even produces benchmark reports (`reports/`) — you generated evidence and then never explained it to a human being.

### 10. You fail the 8-second test 🟡

What a recruiter actually saw, in order, on the old README:

1. Six lines of ASCII art
2. Three lines of typing animation
3. Four badges about *feelings* (FOLLOWERS / STATUS / FOCUS / CERTIFIED)
4. A fake terminal with a boxed name card
5. Two paragraphs of philosophy

**First hard fact about your skills: ~620 pixels down.** Most screens are 800. You spent your entire above-the-fold on vibes. The aesthetic is good and worth keeping — but a recruiter decides in 8 seconds whether to scroll, and you gave them nothing to decide on.

---

## What's genuinely strong — don't lose this

I'm not being nice, these are the things I'd defend to a hiring committee:

1. **Packet-level work is hard and you actually did it.** Most graduates have CRUD apps and a certificate. You have a live-capture IDS with six detection classes, per-source alert cooldowns and tunable thresholds — that's the shape of real detection engineering, not a tutorial.
2. **You built a scanning framework instead of wrapping Nmap.** The `--scan-type syn` raw-socket engine and 9 protocol version probes are legitimately non-trivial.
3. **RHCSA is respected.** A hands-on Linux exam carries more weight with infra/security leads than three multiple-choice certs. You devalue it by not linking verification.
4. **~8,900 lines of Python** across four real projects (NIDS 1,900 · VANTA 5,000 · Remote GUI 1,150 · ScanForge 720). That's a real body of work.
5. **You already learned the thing most candidates never learn:** you got an external contributor's PR merged into `Port_Scanner`. Now do it in the other direction.
6. **Your project READMEs are good** — `ScanForge` and `NIDS` have features, structure, examples, legal notes. That's professional instinct. It's just the profile README that was pitched as a landing page instead of a résumé.

---

## Fix list

### In the next 30 minutes

- [ ] **Rotate the secrets** in `Learning-Mangement-System/.env` — new `JWT_SECRET`, new DB password. Assume they're burned.
- [ ] Profile settings: location → **Chennai, India**. Bio → `CS undergrad · builds packet-level security tooling in Python (NIDS, scanners, MTD) · RHCSA · open to security/network engineering roles`. Set your résumé URL as your website.
- [ ] Delete `distributed_graph_processing_unit` — or make it real. An empty repo is worse than no repo.
- [ ] Rename `Learning-Mangement-System` → `Learning-Management-System`.
- [ ] Add descriptions + topics to all 9 repos (copy-paste set below).
- [ ] Remove the HackTheBox badge from your README (done in this branch) until you have a public profile worth linking.

### This week

- [ ] **Purge secrets and artifacts from history** in `Learning-Mangement-System`, `HPC-project`, `VANTA`, `UPI-vanguard`:
  ```bash
  pip install git-filter-repo
  git clone --mirror <repo>.git && cd <repo>.git
  git filter-repo --path .env --path node_modules --path .npm-cache --path __pycache__ --path dist --path models/Fraud_model.pkl --invert-paths
  gitleaks detect --no-git   # confirm clean, then force-push
  ```
- [ ] Add a `.gitignore` to every repo (`__pycache__/`, `.env`, `node_modules/`, `dist/`, `*.pkl`).
- [ ] Commit binaries and models as **GitHub Releases**, not blobs.
- [ ] Add a screenshot + short GIF to NIDS, VANTA and the Remote GUI READMEs. **This is the highest-return hour in this whole list.**

### Next 30 days — the things that actually change your callback rate

- [ ] **Write NIDS tests.** 10 pytest cases minimum: one per detection class, plus threshold-boundary cases. Then wire CI:

  ```yaml
  # .github/workflows/ci.yml — paste into NIDS, ScanForge, VANTA
  name: CI
  on: [push, pull_request]
  jobs:
    test:
      runs-on: ubuntu-latest
      strategy:
        matrix: { python-version: ["3.10", "3.11", "3.12"] }
      steps:
        - uses: actions/checkout@v4
        - uses: actions/setup-python@v5
          with: { python-version: "${{ matrix.python-version }}" }
        - run: pip install -r requirements.txt pytest ruff
        - run: ruff check .
        - run: pytest -q
  ```
  Then add the green badge to the README. **A green CI badge is the cheapest trust signal on your profile** — it proves the code runs on someone else's machine.
- [ ] **Tag `v1.0.0` on NIDS** with release notes. "Shipped" and "has files" are different signals.
- [ ] **Publish three writeups.** One per project, 700–1,200 words, with packet captures and real numbers. "How I detect ARP poisoning with Scapy" will get you more interviews than the repo itself, because it proves you can explain your thinking.
- [ ] **Get one external PR merged.** Start with docs or tests in a small security project (`nmap`, `scapy`, `pwnagotchi`, `suricata` rule docs). One line of merged upstream code inverts deficit #3.
- [ ] **File 3 issues** on tools you use. Real bug reports, with reproductions. Free, fast, and it makes you look like an engineer instead of a consumer.

---

## Copy-paste: repo descriptions & topics

| Repo | Description | Topics |
|---|---|---|
| `Network-Intrusion-Detection-System-NIDS-` | Desktop network IDS in Python — live Scapy capture, 6 detection classes (SYN scan, ICMP/UDP flood, SSH/VNC brute-force, ARP poisoning), SQLite alerting, CSV/PCAP export. | `network-security` `ids` `scapy` `python` `packet-capture` `intrusion-detection` |
| `Port_Scanner` | From-scratch Python port scanning framework — TCP connect + raw-socket SYN engines, 9 protocol version probes, CIDR parsing, JSON output. No Nmap dependency. | `port-scanner` `cybersecurity-tools` `syn-scan` `python3` `reconnaissance` |
| `VANTA-Variable-Network-Topology-Architecture-` | Moving-target network defence: a Python controller that mutates topology and addressing, with an attack simulator and a benchmark suite comparing static vs. mutated networks. | `sdn` `moving-target-defense` `network-security` `python` `benchmarking` |
| `Custom-App-only-remote-GUI-framework` | Application-scoped remote GUI framework (Raspberry Pi ↔ desktop) built to study remote-access attack surfaces — no OS persistence, no background service. | `remote-access` `python` `security-research` `raspberry-pi` |
| `Learning-Management-System` | Full-stack LMS — Node/Express + MySQL, JWT auth, bcrypt hashing, role-based dashboards, file uploads. | `nodejs` `express` `mysql` `jwt` `fullstack` |
| `UPI-vanguard` | UPI transaction fraud detection — scikit-learn model with a CustomTkinter analyst GUI, trained on synthetic transaction logs. | `fraud-detection` `machine-learning` `python` `fintech` |
| `HPC-project` | Distributed graph processing — parallel BFS/Pagerank over edge-list graphs with an HPC visualiser GUI. | `hpc` `graph-processing` `python` `distributed-systems` |

> One-line rule for the future: **no repo goes public without a description, topics, a license, a `.gitignore`, and one screenshot.**

---

## What NOT to add (you told me: no CTFs, no hackathon wins)

Do not add CTF badges, "Top 1% TryHackMe", fake podium lines, or a "Hackathon Winner" section. Recruiters verify these; a security recruiter *loves* verifying these. One fabricated line poisons the four real projects next to it.

You don't need CTFs. You need **substitutes that a non-CTF person can earn in a weekend:**

| Instead of | Do this | Why it works |
|---|---|---|
| CTF podium | TryHackMe: finish 2 learning paths, screenshot the completion badges, link the public profile | Verifiable, public, no competition needed |
| Hackathon win | Publish a **writeup with a working PoC** (e.g. "detecting ARP poisoning on a real home network") | Proof of thought > proof of placement |
| "CVE research" | File 3 real bug reports on open-source security tools | Shows you can read other people's code |
| Skill bars | The evidence table now in your README | Bars are unverifiable; links are not |
| `[NEXT] CTF` in the roadmap | `v1.0 + tests + CI + a release` | Shipping is the rarest student signal there is |

**The one-line pitch you should memorise for interviews, based on what you actually have:**

> "I write packet-level Python. I built an IDS with six detection classes and a raw-socket port scanner from scratch, and I hold RHCSA. I'm looking for a detection or network security role where I can turn that into production rules."

That is true, specific, memorable, and every word is backed by a URL. Use it.

---

*Files changed in this branch: `README.md` (rewritten as a recruiter-scannable, evidence-linked profile), `AUDIT.md` (this file).*
