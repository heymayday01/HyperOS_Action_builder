<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Orbitron&weight=800&size=42&duration=3000&pause=1000&color=FF6700&center=true&vCenter=true&width=700&height=80&lines=HyperOS+Action+Builder" alt="Project Title" />

<h3>⚡ Serverless, GitHub-Action-powered automatic HyperOS ROM porter for Xiaomi devices</h3>

<p>
  <a href="https://github.com/heymayday01/HyperOS_Action_builder/stargazers"><img src="https://img.shields.io/github/stars/heymayday01/HyperOS_Action_builder?style=for-the-badge&color=FF6700&labelColor=0D1117" /></a>
  <img src="https://img.shields.io/github/forks/heymayday01/HyperOS_Action_builder?style=for-the-badge&color=58A6FF&labelColor=0D1117" />
  <img src="https://img.shields.io/github/repo-size/heymayday01/HyperOS_Action_builder?style=for-the-badge&color=3FB950&labelColor=0D1117" />
  <img src="https://img.shields.io/badge/Platform-GitHub%20Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white&labelColor=0D1117" />
  <img src="https://img.shields.io/badge/Target-HAYDN-FF6700?style=for-the-badge&logo=xiaomi&logoColor=white&labelColor=0D1117" />
</p>

<p>
  <img src="https://img.shields.io/badge/Source-FUXI%20%2F%20NUWA%20%2F%20ISHTAR-58A6FF?style=flat-square&logo=xiaomi&logoColor=white" />
  <img src="https://img.shields.io/badge/Target-HAYDN%20(Mi%2011X%20Pro%20%2F%20K40%20Pro%2B%20%2F%20Mi%2011i)-FF6700?style=flat-square&logo=xiaomi&logoColor=white" />
  <img src="https://img.shields.io/badge/Status-Active-3FB950?style=flat-square" />
  <img src="https://img.shields.io/badge/License-MIT-blue?style=flat-square" />
</p>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%" />

</div>

## 📖 Overview

**HyperOS Action Builder** is a serverless ROM porting pipeline that runs entirely on GitHub Actions. It takes official HyperOS ROM images built for Xiaomi's **FUXI**, **NUWA**, and **ISHTAR** devices and automatically repackages them into flashable ROMs for the **HAYDN** family — Mi 11X Pro / K40 Pro+ / Mi 11i.

No servers. No local builds. No paid CI. Fork → trigger → download a ready-to-flash ROM.

> Forked from [ljc-fight/miui_port](https://github.com/ljc-fight/miui_port) — significantly extended and refactored for the GitHub Actions workflow model.

---

## ✨ Features

| Capability | Description |
|------------|-------------|
| 🔄 **One-click porting** | Trigger a workflow run with the source ROM URL — output a HAYDN-compatible zip |
| ☁️ **100% Serverless** | Runs entirely on GitHub Actions — zero local toolchain required |
| 🧩 **Auto-fspatch & contextpatch** | Handles fspatch, contextpatch, and bypass-sign-check automatically |
| 📦 **lpunpack super.img** | Unpacks `super.img` from `payload.bin` and re-packs with target partitions |
| 🔐 **BypassSignCheck** | Allows installation of ported ROMs without breaking signature enforcement |
| 🗂️ **Artifacts retention** | Built ROM uploaded as GitHub release artifact — shareable URL |
| 🛡️ **Idempotent port.sh** | Re-running on the same input produces the same output (no surprises) |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                     GitHub Actions Runner                        │
│                                                                  │
│  ┌─────────────┐    ┌─────────────┐    ┌────────────────────┐  │
│  │  setup.sh   │ →  │  port.sh    │ →  │  Release Artifact  │  │
│  │  (deps)     │    │  (porting)  │    │  (HAYDN-flashable) │  │
│  └─────────────┘    └─────────────┘    └────────────────────┘  │
│         │                  │                                     │
│         ▼                  ▼                                     │
│   apt install         BypassSignCheck                            │
│   python3             fspatch                                    │
│   qemu-utils          contextpatch                               │
│   brotli              lpunpack                                   │
│                       gettype                                    │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🚀 Quick Start

### 1. Fork this repo

Click **Fork** at the top-right of the repo page.

### 2. Trigger a build

Go to the **Actions** tab → select the **HyperOS Port** workflow → **Run workflow** → paste the source ROM URL.

### 3. Download

When the run completes (typically 8–15 minutes), the built HAYDN ROM will be available as a workflow artifact and optionally as a GitHub Release.

---

## 📂 Project Structure

```
HyperOS_Action_builder/
├── .github/
│   └── workflows/
│       └── port.yml          ← GitHub Actions workflow definition
├── bin/                       ← Bundled binaries (fspatch, lpunpack, gettype, ...)
├── port.sh                    ← Main porting script (~52 KB)
├── setup.sh                   ← Runner bootstrap: installs system deps
└── README.md                  ← This file
```

---

## 🛠️ Tech Stack

<p>
  <img src="https://img.shields.io/badge/Shell-121011?style=for-the-badge&logo=gnu-bash&logoColor=white" />
  <img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white" />
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/Ubuntu-22.04-E95420?style=for-the-badge&logo=ubuntu&logoColor=white" />
  <img src="https://img.shields.io/badge/QEMU-FF6600?style=for-the-badge&logo=qemu&logoColor=white" />
</p>

---

## ⚠️ Disclaimer

- Porting ROMs across devices carries inherent risk. **Always back up your data** before flashing.
- This project is not affiliated with Xiaomi, Qualcomm, or Google.
- You are responsible for complying with the source ROM's license terms.
- The maintainers are not liable for bricked devices, voided warranties, or lost data.

---

## 🙏 Credits

This project stands on the shoulders of giants. Ranked in alphabetical order:

| Project | Author | Purpose |
|---------|--------|---------|
| [BypassSignCheck](https://github.com/Weverses/BypassSignCheck) | [@Weverses](https://github.com/Weverses) | Signature verification bypass |
| [contextpatch (TIK)](https://github.com/ColdWindScholar/TIK) | [@ColdWindScholar](https://github.com/ColdWindScholar) | Context-aware patching |
| [fspatch](https://github.com/affggh/fspatch) | [@affggh](https://github.com/affggh) | Filesystem patch tool |
| [gettype](https://github.com/affggh/gettype) | [@affggh](https://github.com/affggh) | File type detection helper |
| [lpunpack](https://github.com/unix3dgforce/lpunpack) | [@unix3dgforce](https://github.com/unix3dgforce) | Unpack `super.img` logical partitions |
| [miui_port](https://github.com/ljc-fight/miui_port) | [@ljc-fight](https://github.com/ljc-fight) | Original MIUI porting scripts — upstream foundation |

---

## 📜 License

MIT — feel free to fork, modify, and redistribute. Pull requests welcome.

---

## 👤 Author

<div align="center">

**Aryan Thakare** — [@heymayday01](https://github.com/heymayday01)

[![GitHub](https://img.shields.io/badge/GitHub-heymayday01-181717?style=for-the-badge&logo=github)](https://github.com/heymayday01)
[![Profile](https://img.shields.io/badge/View-Profile-58A6FF?style=for-the-badge&logo=github&logoColor=white)](https://github.com/heymayday01)

<sub>⭐ If this saved you a weekend of manual porting — give it a star.</sub>

</div>
