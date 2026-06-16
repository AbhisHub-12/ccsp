# Glossary — CSPP Cyber Security Terms

A beginner-friendly A–Z reference of the core terms covered across the Skillogic CSPP cyber security program.

## A

**Access Control** — Rules and mechanisms that decide who (or what) is allowed to view or use a resource, and at what level.

**Adversarial Machine Learning** — Techniques attackers use to fool or manipulate AI/ML models, such as feeding crafted inputs that cause the model to misclassify data.

**AES (Advanced Encryption Standard)** — A widely used symmetric block cipher that encrypts data in 128-bit blocks with key sizes of 128, 192, or 256 bits.

**Anomaly Detection** — A monitoring approach that learns "normal" behavior and flags activity that deviates from it, often used in modern threat detection and AI-driven security.

**APT (Advanced Persistent Threat)** — A stealthy, well-resourced attacker (often state-sponsored) that gains long-term access to a network and remains undetected to steal data over time.

**ARP Poisoning (ARP Spoofing)** — A sniffing attack where forged ARP messages link an attacker's MAC address to a legitimate IP, letting them intercept traffic on a local network.

**Asymmetric Encryption** — Encryption that uses a key pair: a public key to encrypt and a private key to decrypt (or vice versa), removing the need to share a single secret key.

**Authentication** — The process of verifying that a user, device, or system is who or what it claims to be (for example, with a password or certificate).

**Authorization** — Determining what an authenticated user or system is permitted to do or access.

## B

**Backdoor** — A hidden method of bypassing normal authentication to gain access to a system, often left behind by malware or an attacker.

**Black Box Testing** — A penetration test performed with no prior knowledge of the target's internals, simulating an outside attacker.

**Black Hat** — A hacker who breaks into systems with malicious or illegal intent for personal gain or harm.

**Botnet** — A network of compromised computers ("bots" or "zombies") controlled remotely by an attacker, often used to launch DDoS attacks or send spam.

**Brute Force Attack** — An attack that tries every possible password or key combination until the correct one is found.

**Buffer Overflow** — A flaw where a program writes more data to a memory buffer than it can hold, potentially allowing an attacker to execute malicious code.

## C

**Certificate (Digital Certificate)** — An electronic document that binds a public key to an identity and is signed by a trusted Certificate Authority to prove authenticity.

**Certificate Authority (CA)** — A trusted entity that issues and signs digital certificates, vouching for the identity of the certificate holder.

**Cloud Computing** — Delivering computing resources (servers, storage, software) over the internet on demand, typically billed by usage.

**Container** — A lightweight, portable package that bundles an application with its dependencies so it runs consistently across environments (for example, Docker).

**CSRF (Cross-Site Request Forgery)** — A web attack that tricks an authenticated user's browser into sending an unwanted request to a site where they are logged in.

**CVE (Common Vulnerabilities and Exposures)** — A standardized public identifier (for example, CVE-2021-44228) for a specific known security vulnerability.

**CVSS (Common Vulnerability Scoring System)** — An open framework that rates the severity of a vulnerability on a 0–10 scale based on its characteristics and impact.

**CWE (Common Weakness Enumeration)** — A community catalog of common software and hardware weakness types (for example, "improper input validation") that lead to vulnerabilities.

**Cryptography** — The science of protecting information by transforming it so only authorized parties can read or verify it.

## D

**DDoS (Distributed Denial of Service)** — A denial-of-service attack launched from many distributed machines (often a botnet) at once to overwhelm a target.

**Defense in Depth** — A strategy of layering multiple, independent security controls so that if one fails, others still protect the system.

**Digital Signature** — A cryptographic value created with a private key that proves a message's origin and that it has not been altered.

**DNS Poisoning (DNS Spoofing)** — Corrupting DNS responses or cache so that a domain name resolves to an attacker-controlled IP address.

**DoS (Denial of Service)** — An attack that makes a system or service unavailable to legitimate users, typically by flooding it with traffic or requests.

## E

**ECC (Elliptic Curve Cryptography)** — An asymmetric cryptography method based on the math of elliptic curves, offering strong security with smaller keys than RSA.

**EDR (Endpoint Detection and Response)** — Security tooling that continuously monitors endpoints (laptops, servers) to detect, investigate, and respond to threats.

**Encryption** — The process of converting readable data (plaintext) into an unreadable form (ciphertext) so only authorized parties can decrypt it.

**Enumeration** — The active stage of attack where a hacker extracts detailed information (usernames, shares, services) from a target after initial scanning.

**Ethical Hacking** — Legally and with permission testing systems for vulnerabilities the way an attacker would, in order to fix them before criminals exploit them.

**Exploit** — A piece of code or technique that takes advantage of a specific vulnerability to cause unintended behavior such as gaining access.

## F

**Fileless Malware** — Malicious code that runs in memory and abuses legitimate system tools (like PowerShell) instead of writing files to disk, making it hard to detect.

**Firewall** — A security device or software that filters network traffic and allows or blocks it based on a defined set of rules.

**Footprinting** — The first reconnaissance phase of gathering as much information as possible about a target organization or system.

## G

**Grey Box Testing** — A penetration test performed with partial knowledge of the target, blending the perspectives of an insider and an outsider.

**Grey Hat** — A hacker who operates between ethical and malicious, sometimes breaking rules or laws without clear malicious intent.

## H

**Hashing** — A one-way function that converts data into a fixed-length value (a hash) used to verify integrity; it cannot be reversed to the original data.

**Honeypot** — A decoy system deliberately exposed to attract attackers, study their methods, and divert them from real assets.

## I

**IaaS (Infrastructure as a Service)** — A cloud model that provides virtualized computing infrastructure (servers, storage, networking) that customers manage themselves.

**ICS (Industrial Control System)** — Systems that monitor and control industrial processes such as power, water, and manufacturing operations.

**IDS (Intrusion Detection System)** — A monitoring system that detects and alerts on suspicious or malicious network or host activity but does not block it.

**IoT (Internet of Things)** — The network of everyday physical devices (cameras, sensors, appliances) connected to the internet, often with weak built-in security.

**IP (Internet Protocol)** — The core protocol that addresses and routes packets of data between devices across networks.

**IPS (Intrusion Prevention System)** — Like an IDS, but it can actively block or stop detected malicious traffic in real time.

## K

**Kubernetes** — An open-source platform that automates the deployment, scaling, and management of containerized applications across clusters of machines.

## L

**LDAP (Lightweight Directory Access Protocol)** — A protocol for accessing and managing directory information (such as users and groups), commonly enumerated by attackers for account details.

## M

**MAC Flooding** — An attack that overwhelms a switch's MAC address table so it broadcasts traffic to all ports, letting an attacker sniff data.

**Malware** — Any software intentionally designed to cause harm, such as viruses, worms, trojans, and ransomware.

**MITM (Man-in-the-Middle Attack)** — An attack where the attacker secretly intercepts and possibly alters communication between two parties who believe they are talking directly.

## N

**NetBIOS** — A legacy networking service that lets applications on a LAN communicate; it can be enumerated to reveal computer names, shares, and users.

**NIST SP 800-115** — A U.S. NIST guide that provides a technical methodology for planning and conducting security testing and assessments.

**NULL Scan** — A stealth port scan that sends TCP packets with no flags set, using the target's response (or silence) to infer whether ports are open or closed.

## O

**OSINT (Open Source Intelligence)** — Information gathered from publicly available sources (websites, social media, public records) during reconnaissance.

**OSI Model** — A seven-layer conceptual model (Physical, Data Link, Network, Transport, Session, Presentation, Application) that describes how network communication works.

**OSSTMM (Open Source Security Testing Methodology Manual)** — A peer-reviewed methodology that defines a structured, measurable approach to security testing.

**OT (Operational Technology)** — Hardware and software that monitors and controls physical equipment and processes, especially in industrial settings.

**OWASP Top 10** — A regularly updated awareness list from the Open Web Application Security Project ranking the most critical web application security risks.

## P

**PaaS (Platform as a Service)** — A cloud model that provides a ready-made platform (runtime, tools, databases) for developers to build and deploy applications.

**Payload** — The part of malware or an exploit that performs the intended malicious action, such as deleting data or opening a backdoor.

**Penetration Testing (Pen Test)** — An authorized simulated attack on a system to find and demonstrate exploitable vulnerabilities before real attackers do.

**Phishing** — A social engineering attack that uses fraudulent emails or messages to trick victims into revealing credentials or installing malware.

**PKI (Public Key Infrastructure)** — The framework of certificates, authorities, and policies used to create, manage, and validate public keys and digital identities.

**Port** — A numbered communication endpoint on a device that identifies a specific service or process (for example, port 443 for HTTPS).

**Port Scanning** — Probing a target's ports to discover which services are running and which ports are open, closed, or filtered.

**Post-Quantum Cryptography** — New cryptographic algorithms designed to remain secure even against attacks from future quantum computers.

**Pretexting** — A social engineering tactic where the attacker invents a believable scenario or false identity to manipulate a victim into sharing information.

**Privilege Escalation** — Gaining higher access rights than originally granted, either to another user's level (horizontal) or to administrator/root level (vertical).

**Protocol** — An agreed-upon set of rules that governs how devices format, transmit, and receive data over a network.

**PTES (Penetration Testing Execution Standard)** — A standard defining the phases of a penetration test, from pre-engagement and intelligence gathering through reporting.

## R

**Ransomware** — Malware that encrypts a victim's files or systems and demands payment (a ransom) in exchange for the decryption key.

**Reconnaissance** — The initial information-gathering phase of an attack, which can be passive (no direct contact) or active (directly probing the target).

**Rootkit** — Malware designed to hide its presence and maintain privileged (root/admin) access while evading detection.

**RSA** — A widely used asymmetric encryption algorithm based on the difficulty of factoring large prime numbers, used for encryption and digital signatures.

**Rules of Engagement (RoE)** — The agreed-upon scope, limits, methods, and timing that define what a penetration tester is and is not allowed to do.

## S

**SaaS (Software as a Service)** — A cloud model that delivers ready-to-use software over the internet, fully managed by the provider (for example, web email).

**Salt** — Random data added to a password before hashing so that identical passwords produce different hashes, defeating precomputed (rainbow table) attacks.

**SCADA (Supervisory Control and Data Acquisition)** — A type of industrial control system used to remotely monitor and control large-scale infrastructure like pipelines and power grids.

**Session Hijacking** — Taking over a valid user session, often by stealing or guessing the session token, to impersonate the user.

**Shared Responsibility Model** — The cloud security principle that the provider secures the underlying cloud while the customer secures their data, configuration, and usage.

**Smishing** — A phishing attack delivered through SMS text messages.

**Sniffing** — Capturing and inspecting network traffic, which can be passive (just listening) or active (manipulating traffic to intercept it).

**SNMP (Simple Network Management Protocol)** — A protocol for monitoring and managing network devices; weak community strings make it a common enumeration target.

**SOAR (Security Orchestration, Automation, and Response)** — Tools that automate and coordinate security workflows and incident response across multiple systems.

**Social Engineering** — Manipulating people psychologically into revealing information or performing actions that compromise security.

**SQL Injection (SQLi)** — A web attack that inserts malicious SQL into input fields to read, modify, or destroy database data.

**SYN Scan (Half-Open Scan)** — A fast, stealthy port scan that sends a SYN packet and reads the response without completing the full TCP handshake.

**Symmetric Encryption** — Encryption that uses the same secret key to both encrypt and decrypt data, requiring the key to be shared securely.

**System Hacking** — The phase where an attacker gains access to a target system, escalates privileges, executes applications, hides files, and covers their tracks.

## T

**TCP (Transmission Control Protocol)** — A connection-oriented transport protocol that guarantees reliable, ordered delivery of data using a three-way handshake.

**TCP/IP Model** — A four-layer networking model (Link, Internet, Transport, Application) that underpins how the internet communicates.

**Threat** — Any potential cause of an unwanted incident that could harm a system or organization.

**TCP Connect Scan** — A port scan that completes the full TCP three-way handshake to confirm a port is open; reliable but easier to detect.

**Trojan (Trojan Horse)** — Malware disguised as legitimate software that tricks users into running it, then performs malicious actions in the background.

## U

**UDP (User Datagram Protocol)** — A connectionless transport protocol that sends data quickly without guaranteeing delivery or order, used for speed-sensitive services.

## V

**Virus** — Malware that attaches to a legitimate file or program and spreads when that host is executed, requiring user action to propagate.

**Vishing** — A social engineering attack carried out over voice calls to trick victims into revealing sensitive information.

**Vulnerability** — A weakness or flaw in a system, application, or process that an attacker can exploit to compromise security.

## W

**WEP (Wired Equivalent Privacy)** — An outdated and insecure Wi-Fi encryption standard that is easily cracked and should no longer be used.

**White Box Testing** — A penetration test performed with full knowledge of the target's internals, such as source code, architecture, and credentials.

**White Hat** — An ethical hacker who tests systems legally and with permission to improve security.

**Worm** — Self-replicating malware that spreads across networks on its own, without needing to attach to a host file or rely on user action.

**WPA / WPA2 / WPA3** — Successive Wi-Fi Protected Access security standards; WPA replaced WEP, WPA2 added stronger AES encryption, and WPA3 further hardened authentication and encryption.

**WPS (Wi-Fi Protected Setup)** — A feature meant to simplify connecting devices to Wi-Fi, but its PIN method is vulnerable to brute-force attacks.

## X

**Xmas Scan** — A stealth port scan that sets the FIN, PSH, and URG TCP flags (lighting up the packet "like a Christmas tree") to probe port states.

**XSS (Cross-Site Scripting)** — A web attack that injects malicious scripts into trusted web pages so they run in other users' browsers, stealing data or hijacking sessions.

## Z

**Zero-Day** — A vulnerability that is unknown to the vendor and has no available patch, leaving systems exposed until a fix is released.
