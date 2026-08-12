# Task 4 *Research Report: Common Network Security Threats*

## Introduction

Network security has become an important part of almost every organization. Today, companies depend on cloud services, websites, APIs, remote employees, and wireless networks. This also gives attackers more opportunities to target them.

A small security weakness, such as an unpatched system, a misconfigured server, or an unsafe Wi-Fi network, can sometimes lead to serious problems. Attackers may use these weaknesses to interrupt services, steal information, or redirect users to fake websites. Some common network threats are **DoS/DDoS attacks, Man-in-the-Middle attacks, IP spoofing, and DNS poisoning**. Understanding these threats helps organizations choose the right security measures to protect their networks.

---

## 1. DoS / DDoS Attacks

### How it works

A **Denial-of-Service (DoS)** attack tries to make a website, server, or network unavailable by sending more traffic or requests than it can handle.

A **Distributed Denial-of-Service (DDoS)** attack works in the same way, but the traffic comes from many devices at the same time. Attackers may use compromised computers or other internet-connected devices.

One common method is an **amplification attack**, where attackers misuse poorly configured services such as DNS or Memcached to generate much larger amounts of traffic toward the target.

### Real-world example

In February 2018, **GitHub** experienced a major DDoS attack that reached about **1.35 Tbps**. Attackers used publicly exposed Memcached servers to amplify the traffic. GitHub experienced disruption for around 10 minutes, but there was no reported compromise of user data.

### Impact

* Websites and online services may become unavailable.
* Organizations can lose money because of downtime.
* Customers may lose trust in the company.
* Other networks can also be affected by large-scale attacks.

### Mitigation strategies

1. Use rate limiting and traffic filtering.
2. Use DDoS protection services and CDNs.
3. Disable or secure unnecessary internet-facing services.
4. Monitor network traffic for unusual activity.

---

## 2. Man-in-the-Middle (MITM) Attacks

### How it works

In a **Man-in-the-Middle (MITM)** attack, an attacker secretly gets between two systems that are communicating. The attacker may be able to observe or modify the information being exchanged.

For example, an attacker could create a fake Wi-Fi network that looks legitimate. If someone connects to it, the attacker may be able to monitor their network traffic. Other techniques include ARP spoofing and exploiting weak certificate validation.

### Real-world example

The **DigiNotar breach in 2011** is a well-known example related to MITM attacks. Attackers gained the ability to create fraudulent digital certificates for websites. These certificates could make fake websites appear trustworthy and could potentially allow secure communications to be intercepted.

### Impact

* Usernames and passwords may be stolen.
* Personal or financial information can be exposed.
* Sessions may be hijacked.
* Information being exchanged can be modified.

### Mitigation strategies

1. Use HTTPS and enable HSTS.
2. Properly validate digital certificates.
3. Avoid using untrusted networks for sensitive activities.
4. Use VPNs when appropriate.
5. Use network security controls such as dynamic ARP inspection.

---

## 3. IP Spoofing

### How it works

**IP spoofing** means changing the source IP address of a network packet so that it appears to come from another device.

Attackers can use spoofing to hide the actual source of traffic or make traffic appear to come from a trusted system. It is also commonly used in reflection-based DDoS attacks.

### Real-world example

In the **2013 Spamhaus attack**, attackers used spoofed IP addresses when sending requests to open DNS resolvers. Thousands of misconfigured DNS servers responded to the requests, creating a much larger amount of traffic directed toward Spamhaus.

### Impact

* Makes it difficult to identify the real attacker.
* Can be used to support DDoS attacks.
* May bypass weak IP-based security controls.
* Reduces trust in network communication.

### Mitigation strategies

1. Use ingress and egress filtering.
2. Enable anti-spoofing features on routers and firewalls.
3. Use authentication mechanisms such as IPsec where appropriate.
4. Regularly review firewall and access-control rules.

---

## 4. DNS Poisoning / Spoofing

### How it works

**DNS poisoning** occurs when false information is placed into a DNS resolver's cache. DNS normally converts a website name, such as a domain name, into an IP address. If the DNS information is changed, users may be sent to a fake website instead of the real one.

This can be especially dangerous because the fake website may look almost identical to the original website.

### Real-world example

In **2008, security researcher Dan Kaminsky discovered a serious DNS vulnerability**, commonly known as the Kaminsky bug. The vulnerability could allow attackers to insert fake DNS information into vulnerable resolvers. Major DNS software vendors released security updates to protect against the problem.

### Impact

* Users can be redirected to fake websites.
* Login credentials may be stolen.
* Attackers may distribute malware through fake websites.
* Users may lose trust in DNS services.

### Mitigation strategies

1. Use **DNSSEC** to verify DNS records.
2. Use randomized source ports and transaction IDs.
3. Keep DNS software updated.
4. Restrict unnecessary recursive DNS queries.
5. Monitor DNS traffic for unusual activity.

---

## Comparison of Common Network Security Threats

| Threat            | Attack Vector                      | Who Is at Risk?                                         | Difficulty  | Ease of Mitigation |
| ----------------- | ---------------------------------- | ------------------------------------------------------- | ----------- | ------------------ |
| **DoS / DDoS**    | Traffic flooding or amplification  | Websites, APIs, online services                         | Low–Medium  | Medium             |
| **MITM**          | Intercepting network communication | Users on untrusted networks and vulnerable applications | Medium      | Medium–High        |
| **IP Spoofing**   | Forging source IP addresses        | Networks with weak filtering                            | Low–Medium  | Medium             |
| **DNS Poisoning** | Injecting false DNS information    | Organizations and users relying on DNS                  | Medium–High | High               |

---

## Conclusion

Network security threats are not just theoretical problems. Organizations of all sizes can be affected if their systems and networks are not properly protected.

The examples of GitHub, Spamhaus, and DigiNotar show that attackers can take advantage of simple weaknesses and turn them into serious incidents. There is no single security solution that can prevent every attack. Instead, organizations should use **defense in depth**, combining firewalls, encryption, traffic monitoring, access controls, patching, and secure network configurations.

Regularly checking for misconfigured or unnecessary services is also important. By identifying weaknesses early and applying appropriate security controls, organizations can reduce the chances of an attack and limit the damage if an incident occurs.

---

## References

1. National Institute of Standards and Technology (NIST) – Network and DDoS security guidance.
2. Cybersecurity and Infrastructure Security Agency (CISA) – DDoS and network security guidance.
3. MITRE ATT&CK – Network Denial of Service and Adversary-in-the-Middle techniques.
4. GitHub Engineering Blog – February 2018 DDoS incident.
5. Krebs on Security – Coverage of major network security incidents.
6. IBM Security – Man-in-the-Middle attack information.
7. SANS Institute – Network Security and DNS/MITM resources.
8. The Hacker News – Coverage of the 2013 Spamhaus DDoS attack.

---

**Author:**
**Janani R**
**Security Analyst**

