# Hi, I'm Aymen 👋

**Security researcher & bug bounty hunter** · Telecom master's student · Algeria

I find broken authorization in APIs, mobile apps and 5G cores.

- **Bug bounty:** BOLA / BFLA in Android APK and API pentesting on HackerOne, Bugcrowd and Intigriti.
- **Research:** BOLA / BFLA in APIs and SBI authorization in 5G core networks, mapped against 3GPP TS 33.501.
- **Highlight:** a four-CVE Magma chain, from a normal NMS user to full control-plane takeover (**CVSS 3.1 9.9 Critical**), plus a **9.1 Critical** unauthenticated free5GC BSF.
- **Currently:** working toward HTB CPTS.

![Security Research](https://img.shields.io/badge/Focus-BOLA%20%2F%20BFLA%20%7C%20APK%20%26%20API%20%7C%205G%20SBI-blue)
![CVEs](https://img.shields.io/badge/Published%20CVEs-8-red)
![Bug Bounty](https://img.shields.io/badge/Bug%20Bounty-HackerOne%20%7C%20Bugcrowd%20%7C%20Intigriti-green)

---

## Bug Bounty

Focus: BOLA / BFLA in Android APK and API targets (static and dynamic APK analysis, traffic interception, API authorization testing).

- **City of Vienna (Bugcrowd):** ranked **39th on the [Hall of Fame](https://bugcrowd.com/engagements/city-of-vienna-mbb-og/hall_of_fames) from a single P1**, a time-based blind SQL injection on a mobile API.
- Accepted findings on HackerOne, Bugcrowd and Intigriti, including JWT and IDOR issues.
- Handles: `aymenbenlamari` (HackerOne) / `aymencdm` (Bugcrowd, GitHub)

---

## Published CVEs

### free5GC

| CVE | Target | Vulnerability | CWE | CVSS | Advisory | Write-up |
|-----|--------|---------------|-----|------|----------|----------|
| **CVE-2026-115926** | free5GC BSF (≤ `1754bde`, v4.2.3) | Complete absence of authentication on all `/nbsf-management/v1` endpoints. An unauthenticated attacker can create, read, modify and delete PCF bindings, redirecting SMF policy traffic to a rogue PCF | CWE-306 | **9.1 Critical** | [GHSA-5wxg-mj2c-p9p2](https://github.com/free5gc/free5gc/security/advisories/GHSA-5wxg-mj2c-p9p2) | [Write-up](https://github.com/aymencdm/CVE-2026-115926-free5gc-bsf-missing-auth/) |
| **CVE-2026-115925** | free5GC (v1.0.0 – v4.2.3+) | Root CA private key (`cert/root.key`) committed to the repository, allowing anyone to forge certificates trusted by the default NF PKI | CWE-321 | **8.7 High** | [GHSA-grjj-c27p-3mgc](https://github.com/free5gc/free5gc/security/advisories/GHSA-grjj-c27p-3mgc) | [Write-up](https://github.com/aymencdm/CVE-2026-115925-free5gc-root-ca-key-exposure) |

### Magma (NMS + Orc8r)

Four CVEs chain together: a normal NMS user (role=0) becomes SUPERUSER, then gains full Orc8r control-plane access. Chain score: **CVSS 3.1 9.9 Critical** / **CVSS 4.0 9.4 Critical**. Full chain write-up and PoCs: [magma_pocs](https://github.com/aymencdm/magma_pocs).

The per-CVE scores below are the individual ratings assigned by the CNA (VulDB). They understate the real impact because they score each bug in isolation, not the chain.

| CVE | Target | Vulnerability | CWE | CVSS 4.0 / 3.1 | Advisory | Write-up |
|-----|--------|---------------|-----|----------------|----------|----------|
| **CVE-2026-129357** | Magma NMS (≤ 1.9.0) | Missing role check in `hostOrgMiddleware` lets a normal user add a SUPERUSER to any organization | CWE-862 | **5.3 Medium** / 6.3 | [VDB-437420](https://vuldb.com/vuln/437420) | [Chain write-up](https://github.com/aymencdm/magma_pocs) |
| **CVE-2026-129358** | Magma NMS (≤ 1.9.0) | Stored XSS via organization name, rendered unescaped for every member | CWE-79 | **4.8 Medium** / 2.4 | [VDB-437421](https://vuldb.com/vuln/437421) | [Chain write-up](https://github.com/aymencdm/magma_pocs) |
| **CVE-2026-129359** | Magma Orc8r (≤ 1.9.0) | Hardcoded gRPC client-cert token, identical across deployments, accepted by certifier, accessd, configurator and state | CWE-798 | **6.9 Medium** / 7.3 | [VDB-437422](https://vuldb.com/vuln/437422) | [Chain write-up](https://github.com/aymencdm/magma_pocs) |
| **CVE-2026-129360** | Magma Orc8r / obsidian (≤ 1.9.0) | Operator identity taken from the client-supplied `X-Magma-Client-Cert-Serial` header without verifying mTLS | CWE-290 | **6.9 Medium** / 7.3 | [VDB-437423](https://vuldb.com/vuln/437423) | [Chain write-up](https://github.com/aymencdm/magma_pocs) |

### Krill (NLnet Labs)

| CVE | Target | Vulnerability | CWE | CVSS | Advisory | Write-up |
|-----|--------|---------------|-----|------|----------|----------|
| **CVE-2026-109140** | Krill (fixed in 0.16.1) | Login-session tokens are encrypted with a nonce built from a counter that resets to 0 on every restart, so the same (key, nonce) pair is reused after each restart. Any user who can log in can forge an "admin" token | CWE-323 | **8.4 High** (3.1) | [NLnet Labs advisory](https://www.nlnetlabs.nl/downloads/krill/CVE-2026-109140.txt) / [GHSA-7mpx-94gm-vm7j](https://github.com/advisories/ghsa-7mpx-94gm-vm7j) | Coming soon |

### WordPress plugins

| CVE | Target | Vulnerability | CWE | CVSS | Advisory | Write-up |
|-----|--------|---------------|-----|------|----------|----------|
| **CVE-2026-92424** | Content Egg (< 11.9.0) | Contributor+ stored XSS via the import queue. Missing preset authorization plus impersonation of the preset author lets scripts bypass kses | CWE-79 | **6.8 Medium** | [WPScan](https://wpscan.com/vulnerability/917b8042-b38c-4b6a-9237-1dd08ada157d/) | [Write-up](https://github.com/aymencdm/cve-2026-92424-content-egg-stored-xss-) |

## Other Research

- **Final-year thesis (PFE):** comparative, systematic audit of BOLA / BFLA and SBI authorization in Open5GS and free5GC against 3GPP TS 33.501.
- **Magma chain research:** a four-CVE attack chain from a low-privilege NMS account to full Orc8r control-plane compromise, disclosed through VulDB after the project's GitHub advisory process stalled.
- **Krill (RPKI CA):** credited by NLnet Labs as a finder of the login-token nonce reuse (CVE-2026-109140), alongside Anthropic and Ada Logics.

## Skills

**Security**
- BOLA / BFLA and broken access control in APIs
- Android APK static and dynamic analysis, mobile traffic interception
- 5G core / SBI security, 3GPP TS 33.501
- Source code audit (whitebox), penetration testing (blackbox & whitebox)
- Web & API testing (IDOR, broken auth, XSS, SQLi, SSRF)

**Languages & Systems**
- Python, C
- Linux, Bash
- Git
- Embedded: Raspberry Pi, Arduino

**Tooling**
- Burp Suite, Caido for blackbox testing
- Docker & docker-compose for reproducible vulnerable labs and PoCs
- Code audit combined with blackbox tools for whitebox testing

**Background**
- Electronics baccalaureate
- Master's student in telecommunications
- Studying for HTB CPTS

## Methodology

1. **Build a lab**: spin up the target in Docker Compose so every finding has a reproducible environment.
2. **Audit the code**: trace trust boundaries and compare how sibling components implement the same control (for example, auth middleware present in every NF except one).
3. **Confirm black-box**: prove it with Burp/Caido/curl against the running lab.
4. **Disclose responsibly**: private advisory first, CVE through the maintainers or a CNA, public write-up after.

## Side Project

**[medical_autonome](https://github.com/aymencdm/medical_autonome)**: my final-year electronics project, an autonomous hospital medicine-delivery robot (Arduino line following with PID, Raspberry Pi face recognition, Flutter control app).

## Contact

- GitHub: [@aymencdm](https://github.com/aymencdm)
- Bug bounty handles: `aymenbenlamari` / `aymencdm`
- Email: aymenbenlamari@gmail.com
