# Cyber Security Professional Plus (CSPP) — Deep Study Notes

> Beginner-friendly, in-depth notes for the **Skillogic Cyber Security
> Professional Plus (CSPP)** program — 5 courses, 33 modules. Written so that
> someone brand-new to cyber security can read a module and genuinely
> *understand* the topic: what it is, how the attack/defense works, real-world
> examples, the tools, a hands-on lab, and how to defend against it.

---

## ⚠️ Ethics & Legal Notice (read first)

These notes teach offensive techniques **for defensive understanding,
authorized penetration testing, and education only**.

- **Only ever practice on systems you own or are explicitly authorized to
  test** — your own lab, intentionally-vulnerable VMs (Metasploitable, DVWA,
  OWASP Juice Shop), or sanctioned platforms (TryHackMe, Hack The Box).
- Unauthorized access, scanning, or attacks against systems you don't own are
  **illegal** in most jurisdictions (e.g., the US Computer Fraud and Abuse
  Act, the UK Computer Misuse Act, India's IT Act 2000).
- The "Hands-on / Lab" sections are written for **isolated lab environments**,
  never against real or third-party targets.

Knowing how attacks work is what lets you stop them. Use it responsibly.

---

## How to use these notes

- Start with **[Networking Basics](01-networking-basics/)**, then work down through **Course 1 → 5** — each course builds on the last.
- Every module is a self-contained file following the same structure:
  **Intro → Core Concepts → How It Works (+ diagram) → Real-World Examples →
  Tools → Hands-on Lab → Countermeasures → Key Terms → Summary**.
- Diagrams are written in **Mermaid** and render automatically on GitHub.
- New terms are explained inline and collected in [GLOSSARY.md](GLOSSARY.md).
- **Hands-on depth scales with the course level** — gentle in the Foundation,
  progressively more advanced through Level 2 and Penetration Testing.

---

## Program at a glance

| # | Course / section | Code | Modules | Focus |
|---|------------------|------|---------|-------|
| 01 | [Networking Basics](01-networking-basics/) | — | 1 ref | **Start here** — standalone deep networking handbook (foundation for everything else) |
| 02 | [Ethical Hacking Foundation](02-ethical-hacking-foundation/) | SKL-CEF-705 | 6 | The vocabulary, mindset, and map of the whole field |
| 03 | [Professional Level 1](03-professional-level-1/) | SKL-CSP1-710 | 8 | Recon → scanning → exploitation fundamentals |
| 04 | [Professional Level 2](04-professional-level-2/) | SKL-CSP2-711 | 12 | Web, wireless, mobile, cloud, crypto, IoT attacks |
| 05 | [Penetration Testing](05-penetration-testing/) | SKL-PEN-712 | 2 | Running a professional engagement end-to-end |
| 06 | [AI for Cyber Security](06-ai-for-cyber-security/) | SKL-AICS-720 | 5 | Using machine learning to attack and defend |

**Total:** 33 modules + 1 networking reference · ~200 learning hours · 4-month program.

> ℹ️ Folder numbers now run `01`–`06`: **`01-networking-basics`** comes first as
> the recommended starting point, followed by the five official CSPP courses
> (whose course codes `SKL-…` remain the curriculum's source of truth).

---

## Full module index

### 01 · Networking Basics (start here)
- 🌐 [Networking Basics — Deep Reference](01-networking-basics/networking-basics.md) — OSI/TCP-IP, TCP vs UDP, DNS/ARP, DHCP, IPv4 vs IPv6, switching, topologies, VLAN/VPN, firewall, NAT, SSH (with per-topic video links)

### 02 · Ethical Hacking Foundation (`SKL-CEF-705`)
1. [Introduction to Ethical Hacking](02-ethical-hacking-foundation/module-01-introduction-to-ethical-hacking.md)
2. [Introduction to Cyber Security](02-ethical-hacking-foundation/module-02-introduction-to-cyber-security.md)
3. [Cyber Security Key Concepts](02-ethical-hacking-foundation/module-03-cyber-security-key-concepts.md)
4. [Cyber Security Tools Intro](02-ethical-hacking-foundation/module-04-cyber-security-tools-intro.md)
5. [Exploitation and Penetration Testing](02-ethical-hacking-foundation/module-05-exploitation-and-penetration-testing.md)
6. [Network Basics: OSI & TCP/IP Models](02-ethical-hacking-foundation/module-06-network-basics-osi-and-tcp-models.md)
   - 🌐 *Companion:* [Networking Basics — Deep Reference](01-networking-basics/networking-basics.md)

### 03 · Professional Level 1 (`SKL-CSP1-710`)
1. [Cyber Security Introduction & Kali Setup](03-professional-level-1/module-01-cyber-security-introduction.md)
2. [Footprinting and Reconnaissance](03-professional-level-1/module-02-footprinting-and-reconnaissance.md)
3. [Scanning Networks](03-professional-level-1/module-03-scanning-networks.md)
4. [Enumeration](03-professional-level-1/module-04-enumeration.md)
5. [Vulnerability Analysis](03-professional-level-1/module-05-vulnerability-analysis.md)
6. [System Hacking](03-professional-level-1/module-06-system-hacking.md)
7. [Malware Threats](03-professional-level-1/module-07-malware-threats.md)
8. [Sniffing](03-professional-level-1/module-08-sniffing.md)

### 04 · Professional Level 2 (`SKL-CSP2-711`)
1. [Social Engineering](04-professional-level-2/module-01-social-engineering.md)
2. [Denial-of-Service](04-professional-level-2/module-02-denial-of-service.md)
3. [Session Hijacking](04-professional-level-2/module-03-session-hijacking.md)
4. [Evading IDS, Firewalls & Honeypots](04-professional-level-2/module-04-evading-ids-firewalls-and-honeypots.md)
5. [Hacking Web Servers](04-professional-level-2/module-05-hacking-web-servers.md)
6. [Hacking Web Applications](04-professional-level-2/module-06-hacking-web-applications.md)
7. [SQL Injection](04-professional-level-2/module-07-sql-injection.md)
8. [Hacking Wireless Networks](04-professional-level-2/module-08-hacking-wireless-networks.md)
9. [Hacking Mobile Platforms](04-professional-level-2/module-09-hacking-mobile-platforms.md)
10. [Cloud Computing Security](04-professional-level-2/module-10-cloud-computing-security.md)
11. [Cryptography](04-professional-level-2/module-11-cryptography.md)
12. [IoT & OT Hacking](04-professional-level-2/module-12-iot-and-ot-hacking.md)

### 05 · Penetration Testing (`SKL-PEN-712`)
1. [Penetration Testing Fundamentals](05-penetration-testing/module-01-penetration-testing-fundamentals.md)
2. [Penetration Testing Concepts](05-penetration-testing/module-02-penetration-testing-concepts.md)

### 06 · AI for Cyber Security (`SKL-AICS-720`)
1. [Fundamentals of AI in Cyber Security](06-ai-for-cyber-security/module-01-fundamentals-of-ai-in-cyber-security.md)
2. [AI for Threat Detection and Analysis](06-ai-for-cyber-security/module-02-ai-for-threat-detection-and-analysis.md)
3. [AI in Cyber Defence Mechanisms](06-ai-for-cyber-security/module-03-ai-in-cyber-defence-mechanisms.md)
4. [Ethical & Legal Considerations in AI](06-ai-for-cyber-security/module-04-ethical-and-legal-considerations-in-ai.md)
5. [Emerging Trends & Future of AI in Cyber Security](06-ai-for-cyber-security/module-05-emerging-trends-and-future-of-ai.md)
