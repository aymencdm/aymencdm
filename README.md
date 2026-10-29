# Hi, I'm Aymen 👋

**Security researcher & bug bounty hunter** · Telecom master's student · Algeria 🇩🇿

I audit code and break things for a living (well, for bounties). My research focus is **5G core network security**: finding authentication and authorization failures in open-source 5G core implementations, and mapping them against 3GPP TS 33.501.

![Security Research](https://img.shields.io/badge/Focus-5G%20Core%20Security-blue)
![CVEs](https://img.shields.io/badge/Published%20CVEs-3-red)
![Bug Bounty](https://img.shields.io/badge/Bug%20Bounty-HackerOne%20%7C%20Bugcrowd%20%7C%20Intigriti-green)

---

## Published CVEs

| CVE | Target | Vulnerability | CWE | CVSS | Advisory |
|-----|--------|---------------|-----|------|----------|
| **CVE-2026-115926** | free5GC BSF (≤ `1754bde`, v4.2.3) | Complete absence of authentication on all `/nbsf-management/v1` endpoints. An unauthenticated attacker can create, read, modify and delete PCF bindings, redirecting SMF policy traffic to a rogue PCF | CWE-306 | **9.1 Critical** | [GHSA-5wxg-mj2c-p9p2](https://github.com/free5gc/free5gc/security/advisories/GHSA-5wxg-mj2c-p9p2) |
| **CVE-2026-115925** | free5GC (v1.0.0 – v4.2.3+) | Root CA private key (`cert/root.key`) committed to the repository, allowing anyone to forge certificates trusted by the default NF PKI | CWE-321 | **8.7 High** | [GHSA-grjj-c27p-3mgc](https://github.com/free5gc/free5gc/security/advisories/GHSA-grjj-c27p-3mgc) |
| **CVE-2026-92424** | Content Egg WordPress plugin (< 11.9.0) | Contributor+ stored XSS via the import queue. Missing preset authorization plus impersonation of the preset author lets scripts bypass kses | CWE-79 | 6.8 Medium | [WPScan](https://wpscan.com/vulnerability/917b8042-b38c-4b6a-9237-1dd08ada157d/) |

## Other Research

- **Final-year thesis (PFE)**: comparative, systematic audit of 5G core SBI authorization in Open5GS and free5GC against 3GPP TS 33.501.
- **Bug bounty**: accepted findings on Bugcrowd, HackerOne and Intigriti programs, including a P1 SQL injection and JWT/IDOR issues.

## Electronics Project

**[medical_autonome](https://github.com/aymencdm/medical_autonome)** is my final-year electronics project: an autonomous hospital medicine-delivery robot.

- **Arduino Uno** handles line following with 5 IR sensors and PID control through an L298N motor driver.
- **Raspberry Pi 4** (Python) runs face tracking and face recognition on pan/tilt servos, and drives a servo-actuated medicine carousel and door.
- **Flutter desktop app** manages patients, medicines and assignments, with a live camera feed and an emergency stop, talking to the Pi over a REST API and WebSocket.
- The robot is coordinated by a finite state machine: follow line → stop at marker → recognize patient → dispense → resume. Arduino and Pi communicate over a serial protocol.

## Skills

**Security**
- Source code audit (whitebox)
- Penetration testing (blackbox & whitebox)
- 5G core / SBI security, 3GPP TS 33.501
- Web & API testing (IDOR, broken auth, XSS, SQLi, SSRF)

**Languages & Systems**
- Python, C
- Linux, Bash
- Git
- Raspberry Pi (Python, GPIO, camera/vision, servo control)
- Arduino (C/C++, sensors, PID control, motor drivers, serial communication)

**Tooling**
- Burp Suite, Caido for blackbox testing
- Docker & docker-compose for reproducible vulnerable labs and PoCs
- Code audit combined with blackbox tools for whitebox testing

**Background**
- Electronics baccalaureate
- Master's student in telecommunications

## Methodology

1. **Build a lab**: spin up the target in Docker Compose so every finding has a reproducible environment.
2. **Audit the code**: trace trust boundaries and compare how sibling components implement the same control (for example, auth middleware present in every NF except one).
3. **Confirm black-box**: prove it with Burp/Caido/curl against the running lab.
4. **Disclose responsibly**: private advisory first, CVE through the maintainers or a CNA, public write-up after.

## Contact

- GitHub: [@aymencdm](https://github.com/aymencdm)
- Bug bounty handles: `aymenbenlamari` / `aymencdm`
- email : aymenbenlamari@gmail.com

<!-- Add: email, LinkedIn, and a "Currently looking for" line (PhD / telecom AppSec roles) if you want it public. -->
