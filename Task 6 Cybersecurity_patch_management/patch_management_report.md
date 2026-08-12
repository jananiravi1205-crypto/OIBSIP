# Task 6  Research Report: The Importance of Patch Management

---

## Introduction

Patch management is the process of identifying, testing, and installing updates that fix security weaknesses in operating systems, applications, and firmware.

Regular patching is important because attackers often target **known vulnerabilities** for which security updates are already available. If an organization delays patching, attackers may get an opportunity to exploit those weaknesses.

Two well-known examples are the **Equifax breach (2017)** and the **WannaCry ransomware attack (2017)**. In both cases, security patches were available before the major incidents occurred. This shows that patch management is not just an IT task; it is an important part of overall network security.

---

## 1. Why Patch Management Is Important

Software vulnerabilities are discovered regularly by security researchers, vendors, and attackers. These vulnerabilities are often assigned a **CVE (Common Vulnerabilities and Exposures)** number so they can be easily identified.

The **CVSS (Common Vulnerability Scoring System)** is used to measure the severity of vulnerabilities on a scale from 0.0 to 10.0.

| Severity | CVSS Score |
| -------- | ---------: |
| Low      |    0.1–3.9 |
| Medium   |    4.0–6.9 |
| High     |    7.0–8.9 |
| Critical |   9.0–10.0 |

Organizations can use these ratings, along with business impact and whether a vulnerability is being actively exploited, to decide which patches should be applied first.

---

## 2. Real-World Examples

### Equifax Data Breach – 2017

The **Equifax breach** affected approximately 147 million people. The attack exploited **CVE-2017-5638**, a critical vulnerability in Apache Struts.

A security update had already been released before the attack. However, the vulnerable systems were not patched in time.

**Lesson:** Having a security patch available is not enough. Organizations must identify affected systems and install the patch promptly.

### WannaCry Ransomware – 2017

The **WannaCry ransomware attack** spread rapidly across many countries in May 2017. It exploited a vulnerability in Microsoft's SMBv1 protocol known as **EternalBlue**.

Microsoft had released a security update for the vulnerability before the outbreak. However, many systems remained unpatched or were running unsupported software.

**Lesson:** Delayed patching and outdated systems can allow malware to spread quickly across an organization.

---

## 3. Consequences of Not Patching

Failing to install security updates can result in:

* Data breaches and information theft
* Malware and ransomware infections
* Unauthorized system access
* Network disruption and downtime
* Financial losses
* Compliance and legal problems
* Loss of customer trust

A small delay in patching can sometimes become a major security incident if attackers begin exploiting the vulnerability.

---

## 4. Patch Management Lifecycle

Patch management should be treated as a **continuous process**.

### 1. Discovery

Maintain an updated list of all computers, servers, applications, network devices, and firmware.

### 2. Assessment

Identify vulnerabilities and prioritize them based on severity, exploitability, and business importance.

### 3. Testing

Test patches in a controlled environment before installing them on important production systems.

### 4. Deployment

Deploy patches in stages, starting with a small group of systems before applying them across the organization.

### 5. Verification

Check whether the patches were installed successfully and confirm that the vulnerability has been fixed.

---

## 5. Best Practices

Organizations should follow these practices for effective patch management:

1. Maintain a complete **asset inventory**.
2. Monitor vendor security updates and vulnerability databases.
3. Prioritize critical and actively exploited vulnerabilities.
4. Set clear deadlines for applying patches.
5. Test important patches before deployment.
6. Automate patch deployment where appropriate.
7. Keep backups available before major updates.
8. Regularly scan systems to verify patch status.
9. Replace or isolate unsupported legacy systems.
10. Maintain records of patching activities for auditing.

---

## 6. Common Challenges

### Legacy Systems

Older systems may no longer receive security updates.

**Solution:** Upgrade them when possible or isolate them using network segmentation and restricted access.

### Downtime

Some updates require systems to restart or temporarily stop services.

**Solution:** Schedule maintenance during low-usage periods and use redundant systems where possible.

### Testing

Testing every patch can take time.

**Solution:** Use risk-based testing and prioritize critical security updates.

### Large Number of Vulnerabilities

Organizations may receive many vulnerability notifications every day.

**Solution:** Prioritize vulnerabilities based on severity, exploitability, and the importance of the affected system.

---

## 7. Key Security Recommendations

A strong patch management program should include:

* **Regular vulnerability scanning**
* **Automated patch management**
* **Risk-based prioritization**
* **Secure backup procedures**
* **Asset inventory management**
* **Patch testing and verification**
* **Monitoring of actively exploited vulnerabilities**
* **Regular security audits**

The main goal is simple: **identify vulnerabilities early, apply the appropriate fixes, and verify that the systems are actually protected.**

---

## Conclusion

Patch management is one of the basic but most important parts of network security. Many serious attacks have exploited vulnerabilities for which patches were already available.

The Equifax breach and WannaCry outbreak demonstrate that ignoring or delaying security updates can have serious consequences. Organizations should therefore treat patch management as a continuous security process rather than an occasional maintenance task.

By maintaining an accurate asset inventory, prioritizing critical vulnerabilities, testing updates, deploying patches properly, and verifying the results, organizations can significantly reduce their attack surface and protect their systems and data.

---

## References

1. National Institute of Standards and Technology (NIST) – *SP 800-40 Rev. 4: Guide to Enterprise Patch Management Planning*
2. Cybersecurity and Infrastructure Security Agency (CISA) – *Known Exploited Vulnerabilities Catalog and Patch Management Guidance*
3. MITRE – *Common Vulnerabilities and Exposures (CVE)*
4. FIRST.org – *Common Vulnerability Scoring System (CVSS)*
5. IBM Security – *Cost of a Data Breach Report*
6. UK National Audit Office – *WannaCry and NHS Incident Reports*
7. Ponemon Institute – *Costs and Consequences of Gaps in Vulnerability Response*

---

## Author

**Janani R**
**Security Analyst**

