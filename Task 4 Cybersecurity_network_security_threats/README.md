# Task 4: Research Report: Common Network Security Threats

## 🎯 Objective

This research report explains four common network security threats, how they work, their real-world examples, possible impacts, and basic prevention methods.

---

## 🔐 Threats Covered

### 1. 🚨 DoS / DDoS Attack

**What it is:**
An attack that sends a huge amount of traffic to a server or website, making it slow or unavailable.

**Real-world example:**
🌐 In 2018, GitHub faced a **1.35 Tbps DDoS attack** using exposed Memcached servers.

**Key Points:**

* 📡 Overloads network resources
* 🌐 DDoS uses multiple sources
* ⏱️ Can cause service downtime
* 💰 May cause financial loss

**Protection:**

* 🛡️ Use DDoS protection
* 🚦 Apply rate limiting
* 🔍 Monitor unusual traffic
* 🔧 Secure exposed services

---

### 2. 🕵️ Man-in-the-Middle (MITM)

**What it is:**
An attacker secretly intercepts communication between two systems.

**Real-world example:**
🔒 The **DigiNotar breach (2011)** involved fraudulent digital certificates that could be used to make fake websites appear trusted.

**Key Points:**

* 📶 Can occur on unsafe Wi-Fi
* 🔑 May steal usernames and passwords
* 📄 Can expose sensitive information
* 🔄 Communication may be modified

**Protection:**

* 🔒 Use HTTPS and HSTS
* ✅ Validate certificates
* 🛡️ Use VPNs on untrusted networks
* 🔍 Monitor network activity

---

### 3. 🎭 IP Spoofing

**What it is:**
IP spoofing involves changing the source IP address of a packet to make it appear as if it came from another system.

**Real-world example:**
🌐 During the **2013 Spamhaus attack**, spoofed requests were sent to open DNS resolvers, which helped create a much larger traffic attack.

**Key Points:**

* 🥷 Hides the actual source of traffic
* 💥 Can support DDoS attacks
* 🚧 May bypass weak IP-based controls
* 🔎 Makes investigation more difficult

**Protection:**

* 🛡️ Use ingress and egress filtering
* 🔥 Configure firewalls correctly
* 🔐 Use authentication where appropriate
* 🔍 Regularly review network rules

---

### 4. 🌐 DNS Poisoning / Spoofing

**What it is:**
DNS poisoning inserts false DNS information so users can be redirected from a legitimate website to a fake one.

**Real-world example:**
⚠️ The **Kaminsky DNS vulnerability (2008)** showed how vulnerable DNS resolvers could be manipulated with forged responses.

**Key Points:**

* 🔄 Redirects users to fake websites
* 🔑 Can lead to credential theft
* 🎣 Can support phishing attacks
* ⚠️ Reduces trust in DNS

**Protection:**

* 🔐 Use DNSSEC
* 🔄 Randomize DNS source ports
* 🔧 Keep DNS software updated
* 📊 Monitor DNS activity

---

## 📊 Quick Comparison

| Threat           | 🎯 Main Target        | ⚠️ Main Risk          | 🛡️ Main Protection |
| ---------------- | --------------------- | --------------------- | ------------------- |
| 🚨 DoS/DDoS      | Online services       | Service outage        | DDoS protection     |
| 🕵️ MITM         | Network communication | Data theft            | HTTPS/VPN           |
| 🎭 IP Spoofing   | Network traffic       | Identity hiding/DDoS  | Traffic filtering   |
| 🌐 DNS Poisoning | DNS resolution        | Fake-site redirection | DNSSEC              |

---

## 💡 Key Takeaways

* 🛡️ **Use defense in depth** — never depend on a single security control.
* 🔄 **Keep systems updated** to reduce known vulnerabilities.
* 🔍 **Monitor network traffic** to identify unusual activity early.
* 🔒 **Encrypt communication** using secure protocols.
* ⚙️ **Secure unnecessary or exposed services.**
* 📋 **Regularly audit network configurations.**

---

## 🏁 Conclusion

Network security threats can affect organizations of any size. **DDoS, MITM, IP spoofing, and DNS poisoning** can cause service disruption, data theft, or redirection to malicious websites.

A strong security approach combines **firewalls, encryption, monitoring, access control, patching, and secure configurations**. Regular security checks can help identify weaknesses before attackers take advantage of them.

---

## 📚 References

* 📖 NIST — Network and DDoS Security Guidance
* 🏛️ CISA — DDoS and Network Security Guidance
* 🔎 MITRE ATT&CK — Network Security Techniques
* 🐙 GitHub Engineering — 2018 DDoS Incident
* 🔐 IBM Security — MITM Attack Information
* 📚 SANS Institute — Network Security Resources

---

### 👤 Author

**Janani R**
**Security Analyst** 🔐

