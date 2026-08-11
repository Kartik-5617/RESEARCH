# **Threat Intelligence Report: Top 5 Cyber Attacks Endangering the Global Insurance Industry**

The global insurance industry, encompassing health, life, vehicle, general, third-party administrators (TPAs), brokers, and reinsurance companies, operates at the critical intersection of immense financial liquidity and highly sensitive data repositories. Sector enterprises aggregate vast volumes of Personally Identifiable Information (PII), Protected Health Information (PHI), and corporate financial data, creating a highly lucrative environment for organized cybercrime syndicates and advanced persistent threats. Current threat intelligence indicates that the global cyber insurance market is projected to reach approximately $32.19 billion by 2030, driven by the escalating frequency and sophistication of these precise cyber threats1.  
Recent adversarial behavior reveals a distinct pivot away from opportunistic, scattergun malware campaigns toward highly targeted, systemic attacks designed to maximize both financial extortion and downstream data monetization2. The deep integration of third-party digital supply chains, the widespread deployment of cloud-hosted customer portals, and reliance on interconnected financial clearing systems have drastically expanded the attack surface4. Furthermore, stringent regulatory frameworks amplify the business impact of any data exposure, inadvertently granting threat actors unprecedented leverage during extortion negotiations1.  
This comprehensive analysis deconstructs the top five most dangerous cyber attacks currently compromising the insurance ecosystem. These vectors have been identified and ranked based on their operational frequency, catastrophic financial impact, data breach volume, and profound contemporary relevance to the sector.  
═══════════════════════════════════════════════

# **Multi-Extortion Ransomware**

## **1\. Overview**

Multi-extortion (or double/triple extortion) ransomware represents a sophisticated evolution in cyber extortion. In this model, threat actors do not merely encrypt a victim’s environment to halt business operations; they first exfiltrate massive volumes of sensitive data2. The attackers then threaten to publish, sell, or weaponize this stolen data if the ransom is not paid. Triple-extortion tactics escalate this by incorporating Distributed Denial of Service (DDoS) attacks or directly contacting the insurer’s clients, patients, or stakeholders to apply secondary public pressure7.  
The proliferation of the Ransomware-as-a-Service (RaaS) model has democratized this attack vector. Experienced malware developers lease their sophisticated encryption and exfiltration tools to affiliates, enabling operators with varying technical proficiencies to execute high-impact attacks3. The multi-extortion model guarantees leverage for the attackers; even if an insurance company possesses immutable backups and can restore operations independently, the looming threat of regulatory fines, class-action privacy lawsuits, and total reputational destruction forces many to capitulate to the ransom demands.  
Insurance companies, including TPAs and brokerages, are prime targets because continuous operational uptime is strictly required to process claims and underwrite policies9. More critically, the data they hold—medical histories, financial records, and corporate underwriting intelligence—is immensely valuable on dark web markets. Insurers are also known to hold substantial capital reserves and cyber insurance policies of their own, making them paradoxically attractive targets for financial extortion9.

## **2\. How the Attack Works**

The multi-extortion ransomware lifecycle is a protracted, highly structured progression through the victim's network. Attackers often maintain silent persistence for weeks or months (dwell time) to thoroughly map the network, identify the most sensitive databases, and ensure maximum destruction of backup infrastructure before deploying the final encryption payload.  
Attacker (RaaS Affiliate)  
│  
Reconnaissance (External footprinting, open-source intelligence gathering)  
│  
Crafts Attack (Procuring compromised credentials, tailoring phishing lures)  
│  
Victim Interaction (Employee opens malicious attachment or clicks link)  
│  
Initial Access (Phishing, RDP Compromise, or Infostealer Credential reuse)  
│  
Credential Theft / Malware Execution (Dropping C2 beacons like Cobalt Strike)  
│  
Privilege Escalation (Exploiting local vulnerabilities, dumping LSASS memory)  
│  
Lateral Movement (Moving via SMB/WMI, compromising Domain Controllers)  
│  
Data Exfiltration (Silent outbound transfers via Rclone, Mega, or FTP)  
│  
Business Impact (Mass encryption, operational paralysis, data leak extortion, DDoS)

## **3\. Real-World History**

The insurance sector has witnessed several catastrophic multi-extortion ransomware events in recent years. The table below details three landmark incidents, followed by a deeper analytical narrative of each.

| Organization | Year | Country | Industry | Attack Method |
| :---- | :---- | :---- | :---- | :---- |
| **CNA Financial** | 2021 | USA | Commercial Insurance | Phoenix CryptoLocker |
| **AXA Asia** | 2021 | Multiple (Asia) | Health / General | Avaddon Ransomware |
| **Medibank** | 2022 | Australia | Health Insurance | REvil / BlogXX |

**CNA Financial (2021):** One of the largest commercial insurers in the United States was breached by the Phoenix ransomware group, an entity linked to the sanctioned Russian cybercrime syndicate Evil Corp9. The attack began when an employee downloaded a fraudulent browser update, granting the attackers initial access. The threat actors spent weeks conducting quiet reconnaissance, eventually exfiltrating the personal information of approximately 75,000 individuals before encrypting 15,000 systems globally. CNA’s customer portals, underwriting systems, and email infrastructure were completely disrupted. The firm ultimately paid a record-breaking $40 million ransom to regain operational capability and prevent data leakage9. The incident established a dangerous precedent that large financial institutions will pay nine-figure ransoms if operational disruption is severe enough, while also highlighting the severe legal complexities of paying sanctions-linked entities9.  
**AXA Asia Assistance (2021):** Just days after AXA France announced it would cease covering ransomware payments for its cyber insurance clients, the Avaddon RaaS group breached AXA’s Asia divisions, affecting operations in Thailand, Malaysia, Hong Kong, and the Philippines8. The attackers exfiltrated 3 terabytes of data, including customer identification cards, highly sensitive medical records detailing conditions like HIV and hepatitis, and hospital billing documents. To maximize pressure, Avaddon deployed a combined ransomware and DDoS attack7. The attack underscored that insurers taking public stances against ransom payments will be actively targeted by retaliatory cybercrime syndicates.  
**Medibank (2022):** Australian health insurer Medibank suffered a devastating breach affecting 9.7 million current and former customers. Attackers acquired high-level VPN credentials that a Medibank IT contractor had negligently saved on a personal, malware-infected browser16. The BlogXX/REvil gang bypassed the lateral movement phase entirely using these administrative credentials, deployed backdoors, and exfiltrated 200GB of sensitive health claims data. The attack was discovered when Medibank security teams detected the anomalies and shut down the backdoors, though the exfiltration had already occurred16. Medibank's executive board refused to pay the $9.7 million ransom demand. Consequently, the attackers released highly sensitive medical diagnoses, including data on abortions and drug addiction treatments, causing immeasurable brand damage and triggering severe regulatory scrutiny18.

## **4\. Why the Attack Succeeded**

These systemic failures are rarely the result of highly novel technical wizardry; rather, they succeed due to catastrophic failures in fundamental security controls. Across the sector, flat network architectures permit rapid lateral movement. In the Medibank incident, a human mistake—syncing corporate credentials to a personal, unmanaged device—was compounded by a technical failure: the lack of robust, phishing-resistant Multi-Factor Authentication (MFA) on a high-privileged VPN gateway16. Furthermore, inadequate Endpoint Detection and Response (EDR) tuning allows attackers to dwell for weeks, using legitimate administrative tools (Living off the Land binaries) to silently exfiltrate terabytes of data before the noisy encryption phase is ever initiated.

## **5\. Indicators of Compromise (IOCs)**

The following structured indicators are representative of multi-extortion ransomware campaigns targeting enterprise networks.

| IOC Type | Indicator Value | Description |
| :---- | :---- | :---- |
| **Process** | vssadmin.exe Delete Shadows /All /Quiet | Deletion of Windows Volume Shadow Copies to prevent system recovery8. |
| **Process** | bcdedit /set {default} recoveryenabled No | Disabling Windows automatic recovery features prior to encryption8. |
| **Network** | api.mega.co.nz or pastebin.com (High Volume) | Unexpected, sustained outbound connections to cloud storage providers indicating data exfiltration. |
| **File** | \[a-zA-Z0-9\]{5,6}\_readme\_.txt | Common regular expression pattern for ransom notes dropped into encrypted directories7. |
| **Event Log** | Windows Security Event ID 1102 | The audit log was cleared, indicating active defense evasion by an attacker with administrative rights. |

## **6\. Detection**

Security Operations Center (SOC) teams must leverage a layered, defense-in-depth detection strategy heavily mapped to the MITRE ATT\&CK framework. Security Information and Event Management (SIEM) platforms must monitor for impossible travel, unusual VPN logins during off-hours, and bulk file modification anomalies that indicate encryption. EDR solutions are critical for detecting defense evasion techniques, such as the tampering or uninstallation of antivirus processes, and the execution of known ransomware behaviors (T1486 Data Encrypted for Impact). User and Entity Behavior Analytics (UEBA) plays a pivotal role by baselining normal administrative behavior to flag anomalous data access or lateral movement using compromised credentials (T1078 Valid Accounts). Network Intrusion Detection Systems (IDS) must actively look for Command and Control (C2) beaconing patterns, such as those generated by Cobalt Strike, and flag large data transfers to unauthorized external domains (T1048 Exfiltration Over Alternative Protocol).

## **7\. Prevention**

Preventing multi-extortion ransomware requires a strict adherence to Zero Trust principles. Technical controls must mandate phishing-resistant MFA (such as FIDO2 security keys) for all external and privileged access points17. Network segmentation is paramount; critical databases housing PHI and PII must be isolated from general user endpoints, requiring jump servers for administrative access16. The Principle of Least Privilege (PoLP) must be enforced rigidly, stripping unnecessary administrative rights from standard user accounts. Organizations must maintain immutable, offline backups that cannot be wiped or altered by compromised domain administrators. Finally, security monitoring must evolve to XDR (Extended Detection and Response) capabilities, correlating telemetry across endpoints, identity, and cloud environments to catch precursor activities before the encryption payload is delivered.

## **8\. Incident Response**

The incident response lifecycle must be executed with extreme precision. Identification involves confirming the scope of the encryption, identifying patient zero, and determining the exact exfiltration vectors. Containment is critical: responders must immediately sever external internet connectivity and isolate affected VLANs to halt lateral movement, but they must absolutely *not* reboot encrypted machines, as this destroys volatile memory forensics necessary for decryptor development or attribution. Eradication requires rebuilding compromised infrastructure from known-good images, forcing global password resets, and patching the root cause vulnerabilities. During recovery, organizations restore systems from immutable backups. Most importantly, post-incident workflows must include OFAC sanctions screening and comprehensive legal reviews before any ransom negotiations are even considered, as paying a sanctioned entity carries severe legal consequences9.

## **9\. Key Takeaways**

* **Main Risks:** Total operational paralysis and catastrophic regulatory/reputational damage due to the public leakage of sensitive health and financial data.  
* **Business Impact:** Severe financial loss from business interruption, massive regulatory fines, class-action lawsuits, and potential ransom payments that often stretch into the tens of millions of dollars.  
* **Detection Priorities:** Identifying pre-encryption activities is vital—specifically initial access anomalies, credential dumping (Mimikatz), and data staging for exfiltration.  
* **Prevention Priorities:** The deployment of phishing-resistant MFA, the maintenance of immutable backups, and strict internal network segmentation.

═══════════════════════════════════════════════

# **Supply Chain and MFT Zero-Day Exploits**

## **1\. Overview**

Supply chain attacks targeting Managed File Transfer (MFT) systems represent a systemic vulnerability in the global digital ecosystem. These attacks exploit zero-day vulnerabilities in third-party software used globally by enterprises to securely share sensitive data. Instead of attacking an insurance company directly through its perimeter, threat actors compromise the software vendor or a downstream service provider. This single point of failure grants the attackers unfettered access to the data of hundreds, or even thousands, of interconnected organizations simultaneously.  
Threat actors heavily utilize this vector because exploiting a single MFT vulnerability (such as those found in MOVEit, Accellion, or GoAnywhere) provides exponential returns on their operational investment. One successful exploit bypasses the direct perimeter defenses of the ultimate victims20. The insurance sector is uniquely targeted because it relies heavily on MFT solutions to exchange massive, continuous volumes of PII, financial documents, tax records, and claims data with a complex web of brokers, TPAs, reinsurers, and medical providers4. This dense interconnectivity makes the sector uniquely vulnerable to systemic supply chain failures, where a breach at a minor vendor cascades into a massive data exposure for a major carrier.

## **2\. How the Attack Works**

The attack specifically exploits vulnerabilities within web-facing file transfer applications, typically culminating in Remote Code Execution (RCE) or SQL injection (SQLi). Because these systems are designed to interface with the public internet, traditional perimeter firewalls offer no protection.  
Attacker (e.g., Cl0p Ransomware Gang)  
│  
Reconnaissance (Scanning the internet for specific MFT application signatures)  
│  
Crafts Attack (Developing an exploit for a newly discovered zero-day SQLi)  
│  
Victim Interaction (None required; attack is server-side and automated)  
│  
Initial Access (Bypassing authentication via the SQL injection payload)  
│  
Malware Execution (Deployment of a custom web shell into the web directory)  
│  
Privilege Escalation (Web shell runs under the application's service account)  
│  
Data Enumeration (Querying backend databases for file locations and active session IDs)  
│  
Data Exfiltration (Automated, high-volume downloading of client files via the web shell)  
│  
Business Impact (Mass data extortion, publishing victim names on dark web leak sites)

## **3\. Real-World History**

The impact of MFT zero-day exploits has fundamentally altered how the insurance industry views third-party risk.

| Organization | Year | Country | Industry | Attack Method |
| :---- | :---- | :---- | :---- | :---- |
| **Genworth / TIAA** | 2023 | USA | Life/Financial | MOVEit (CVE-2023-34362) |
| **PBI Research** | 2023 | USA | Pension/Audit | MOVEit (CVE-2023-34362) |
| **Centene / Singtel** | 2021 | Global | Telecom/Health | Accellion FTA |

**MOVEit Mass Exploitation (2023):** In mid-2023, the Cl0p ransomware gang executed a highly sophisticated campaign exploiting a zero-day SQL injection vulnerability (CVE-2023-34362) in Progress Software’s MOVEit Transfer21. This single vulnerability compromised thousands of organizations globally. Major insurance and financial entities, including Genworth Financial, TIAA, Sun Life, and The Hartford, were severely impacted, resulting in the exposure of millions of customer records20. The attack was discovered when organizations noticed anomalous outbound data transfers and unauthorized web shells on their MFT servers. The lesson learned was that patching is insufficient if the vulnerability is a zero-day; continuous anomaly detection is required.  
**PBI Research Services (2023):** Demonstrating the devastating downstream blast radius of supply chain attacks, PBI Research Services—a vendor providing audit and pension services to insurers—was compromised via the same MOVEit vulnerability. This breach subsequently exposed the data of millions of individuals associated with PBI's clients, including major retirement systems and life insurance carriers22. This showcased how third- or fourth-party risk manifests: the insurers themselves did not run the vulnerable software, but their data was stolen nonetheless.  
**Accellion FTA (2021):** A legacy file transfer appliance, Accellion FTA, suffered a series of zero-day exploits. The breach impacted major organizations globally, including health insurer Centene and telecommunications giant Singtel, resulting in the theft of vast quantities of medical and personal data28. The incident highlighted the severe dangers of maintaining legacy infrastructure that is no longer rigorously supported or designed with modern security architectures in mind.

## **4\. Why the Attack Succeeded**

These attacks succeed primarily because MFT systems are inherently designed to sit on the public internet to facilitate external data exchange. When a zero-day vulnerability exists—such as improper input validation leading to SQLi—traditional defenses like firewalls and MFA are entirely bypassed, as the application itself is tricked into executing malicious commands23. Furthermore, organizations often heavily over-privilege these service accounts. Instead of restricting the MFT application to a small, quarantined storage volume, the service accounts often hold broad read/write access to internal corporate storage environments, allowing attackers to reach far deeper into the network than intended.

## **5\. Indicators of Compromise (IOCs)**

The following indicators are strongly associated with MFT web shell deployments.

| IOC Type | Indicator Value | Description |
| :---- | :---- | :---- |
| **File** | human2.aspx | Known web shell name utilized by the Cl0p gang during the MOVEit exploits9. |
| **Network** | High-volume TCP/443 Egress | Massive spikes in outbound HTTPS traffic from a server that normally only receives data. |
| **Log** | SQL syntax in HTTP headers | IIS logs showing UPDATE, SELECT, or UNION commands passed via HTTP X-Forwarded-For or Cookie headers. |
| **Process** | w3wp.exe spawning cmd.exe | The IIS worker process executing command-line interpreters, indicating web shell activity. |

## **6\. Detection**

Detecting zero-day MFT exploits requires an emphasis on behavioral anomalies rather than signature-based antivirus. EDR and File Integrity Monitoring (FIM) should immediately flag any newly created .aspx, .php, or .jsp files in public-facing application directories, which strongly indicates the deployment of a server software component (MITRE T1505 Server Software Component: Web Shell). Web Application Firewalls (WAF) must be configured to inspect encrypted traffic, detecting and blocking common injection payloads and anomalous header manipulations. SIEM platforms should be tuned to alert on unusual data egress spikes, especially from servers that normally experience predictable, scheduled traffic patterns.

## **7\. Prevention**

Prevention in the face of zero-days relies on architectural resilience. Technical controls must include the implementation of strict Web Application Firewalls with deep packet inspection. Organizations must transition away from legacy on-premise file transfer appliances to modernized, heavily audited SaaS alternatives built upon zero-trust architectures. Network segmentation is non-negotiable; MFT servers must be placed in isolated DMZs. Crucially, these servers must be explicitly denied the ability to initiate outbound connections to internal corporate networks, restricting their access solely to required, segmented data repositories. Finally, robust Vendor Risk Management (VRM) programs must enforce rigorous third-party assessments, requiring all software vendors and downstream partners to provide regular penetration testing reports and comprehensive Software Bill of Materials (SBOMs).

## **8\. Incident Response**

Incident response for MFT breaches begins with Identification: reviewing web access logs, IIS logs, and database query logs for explicit indicators of SQL injection and web shell deployment. Containment requires taking the vulnerable application offline immediately and isolating the server at the hypervisor or switch level to prevent lateral movement, while preserving memory states for forensics. Eradication involves applying vendor emergency patches, completely removing all identified web shells, and auditing the system for unauthorized administrative accounts created by the threat actor. During Recovery, the MFT environment should ideally be rebuilt from scratch. Legal and regulatory notification protocols must be executed rapidly, not only for the organization but for all downstream clients whose data was stored on the appliance24.

## **9\. Key Takeaways**

* **Main Risks:** Massive, immediate data exfiltration with zero user interaction required, bypassing standard perimeter security.  
* **Business Impact:** Severe regulatory penalties, class-action lawsuits, and a profound loss of institutional trust due to the systemic exposure of partner and customer data.  
* **Detection Priorities:** Detecting web shell deployment (unauthorized script files in web directories) and anomalous outbound data transfers from DMZ servers.  
* **Prevention Priorities:** Rapid patch management workflows, aggressive WAF tuning, and strict network segmentation for all internet-facing appliances.

═══════════════════════════════════════════════

# **API Vulnerabilities and IDOR (Insecure Direct Object Reference)**

## **1\. Overview**

Insecure Direct Object Reference (IDOR) is a highly prevalent access control vulnerability. It occurs when an application provides direct access to internal objects or files based on user-supplied input without verifying the user's authorization. In the context of APIs and web applications, an attacker can simply manipulate parameters—such as a numerical user ID, account number, or document ID in a URL—to seamlessly access records belonging to other users.  
Threat actors heavily utilize IDOR vulnerabilities because they are notoriously easy to exploit and exceptionally difficult for automated security scanners to detect. Scanners look for syntax errors or traditional code injections, whereas IDOR represents a flaw in the fundamental business logic of the application29. Attackers can easily automate the extraction of millions of records using simple, lightweight scripts.  
Modern insurance companies are prime targets because they process vast amounts of customer data through digital portals, mobile applications, and APIs designed for rapid claims submission, policy review, and health tracking. As insurers rushed through digital transformation, many relied on client-side state hiding rather than rigorous server-side authorization6. If backend authorization checks are weak, these APIs transform into highly lucrative data spigots.

## **2\. How the Attack Works**

The attacker successfully bypasses authorization (verifying what a user is allowed to see) while remaining authenticated (verifying who the user is).  
Attacker (Authenticated user with low privileges)  
│  
Reconnaissance (Intercepting web traffic via proxy like Burp Suite)  
│  
Vulnerability Identification (Noticing predictable URLs: /api/claims?id=1001)  
│  
Parameter Manipulation (Changing the parameter to /api/claims?id=1002)  
│  
Victim Interaction (None; purely backend interaction)  
│  
Authorization Failure (Server fails to check if the attacker actually owns claim 1002\)  
│  
Mass Exploitation (Automated script iterates through IDs 1000 to 9999999\)  
│  
Data Exfiltration (Scraping massive amounts of PII/PHI in JSON or PDF format)  
│  
Business Impact (Data dumped on dark web forums, severe regulatory fines)

## **3\. Real-World History**

IDOR vulnerabilities have led to some of the most voluminous data exposures in the history of the insurance sector.

| Organization | Year | Country | Industry | Attack Method |
| :---- | :---- | :---- | :---- | :---- |
| **Star Health** | 2024 | India | Health Insurance | API IDOR / Telegram Leak |
| **First American** | 2019 | USA | Title Insurance | Document URL IDOR |

**Star Health Insurance (2024):** A highly publicized data breach impacted Star Health Insurance, compromising the personal data of over 31 million customers and 5.7 million claims records. A threat actor operating under the moniker "xenZen" exploited a fundamental IDOR vulnerability in Star Health's API to bypass security layers and exfiltrate 7.24 terabytes of data5. The attacker weaponized this data by creating accessible Telegram chatbots, allowing the public to easily retrieve sensitive customer details on demand. In a sophisticated misdirection attempt, xenZen utilized old, previously compromised credentials belonging to the company's CISO to falsely claim insider involvement, severely dragging the security chief into the public spotlight5. The breach severely impacted the company's stock and eroded immense customer trust.  
**First American Financial (2019):** A massive IDOR vulnerability in the company’s document management web portal exposed 885 million files dating back to 200329. The URLs for highly sensitive title insurance documents—which contained bank routing details, tax records, and Social Security Numbers—were generated sequentially. Consequently, anyone with a standard web browser could modify the document ID number in the URL and view other clients' private records without needing to authenticate31. The SEC subsequently charged the firm with disclosure controls and procedures violations, noting that the company's security personnel had identified the vulnerability months prior but failed to remediate it or inform senior executives34.

## **4\. Why the Attack Succeeded**

These attacks succeed due to a fundamental architectural failure: developers failing to differentiate between authentication and authorization29. Developers often incorrectly assume that if a user cannot see a link in the user interface, they cannot access the backend object. This reliance on "security by obscurity" leaves the API wide open to anyone who manipulates the request directly. Furthermore, the total lack of robust rate-limiting allows attackers to script the scraping of millions of records over several days or weeks without triggering volumetric alarms or locking the account6.

## **5\. Indicators of Compromise (IOCs)**

Because IDOR utilizes legitimate application features, IOCs are heavily behavioral rather than signature-based.

| IOC Type | Indicator Value | Description |
| :---- | :---- | :---- |
| **Network** | Sustained High-Volume HTTP GET | Exceptionally high volumes of HTTP requests directed at specific API endpoints from a single IP or session token. |
| **Web Log** | Sequential Parameter Iteration | Server logs displaying rapid iteration of numerical parameters (e.g., doc\_id=1001, doc\_id=1002). |
| **Application** | Anomalous Object Access | A single user account accessing thousands of unique, unrelated customer records within minutes. |

## **6\. Detection**

Detecting IDOR requires deep application-layer visibility. WAFs and API Gateways must be configured to alert on abnormal request velocities or unusual parameter scraping patterns. SIEM platforms should aggregate web access logs and application logs to detect statistical anomalies—for example, a single authenticated user accessing a statistically improbable number of unique records within a short timeframe. UEBA systems can be highly effective here by baselining user activity; if a low-level policyholder suddenly begins downloading thousands of disparate policy documents that do not belong to them, an immediate alert and session termination should be triggered.

## **7\. Prevention**

Preventing IDOR requires a shift toward secure-by-design development. Technical controls must implement rigorous, object-level authorization checks at the backend logic level for *every single* data request. The application must explicitly verify that the currently authenticated user owns or holds the necessary role to access the exact object requested6. To hinder enumeration, developers must utilize non-sequential, unguessable identifiers (such as UUIDs/GUIDs) instead of predictable, auto-incrementing integers for database records. Finally, strict API rate limiting and behavioral CAPTCHAs must be implemented to prevent automated scraping tools from executing effectively6.

## **8\. Incident Response**

Incident response for IDOR begins with Identification: analyzing API gateway and web server logs to determine the exact extent of the parameter enumeration and quantifying the volume of data exfiltrated. Containment requires temporarily disabling the vulnerable API endpoint or enforcing immediate, aggressive rate-limiting and IP blocking against the attacking addresses. Eradication involves deploying an emergency code patch that enforces robust authorization validation on the vulnerable endpoints. During Recovery, organizations must assess the sensitivity of the exposed data to fulfill legal notification obligations. In highly weaponized cases like the Star Health incident, recovery also involves initiating legal action to force platform providers (like Telegram and Cloudflare) to remove the illegal distribution nodes35.

## **9\. Key Takeaways**

* **Main Risks:** Silent, high-volume data theft that completely bypasses traditional perimeter security mechanisms.  
* **Business Impact:** Severe brand damage, catastrophic loss of customer trust, and heavy regulatory action resulting from negligent software design.  
* **Detection Priorities:** Deep API traffic analytics, specifically focusing on rapid parameter iteration and statistically anomalous high-volume data egress by single users.  
* **Prevention Priorities:** Zero-trust application design, strict Broken Object Level Authorization (BOLA) testing, and the elimination of predictable identifiers.

═══════════════════════════════════════════════

# **Business Email Compromise (BEC) and Funds Transfer Fraud (FTF)**

## **1\. Overview**

Business Email Compromise (BEC) is a highly targeted, sophisticated social engineering attack where a threat actor compromises legitimate corporate email accounts to conduct unauthorized transfers of funds or steal sensitive data3. Frequently, BEC is the direct precursor to Funds Transfer Fraud (FTF), a scheme that manipulates authorized users into wiring money directly to attacker-controlled bank accounts3.  
Attackers heavily favor this vector because it relies on human manipulation and broken organizational processes rather than complex, easily patched technical exploits. This makes BEC incredibly effective and massively lucrative. The FBI's Internet Crime Complaint Center (IC3) reports that BEC scams cost U.S. businesses billions annually (over $2.7 billion in recent reporting years alone), consistently ranking it as the most financially damaging form of cybercrime39.  
The insurance industry is a prime target for BEC because its core business lifecycle—premium collections, massive claims payouts, reinsurance settlements, and M\&A brokerage—involves constant, high-value wire transfers38. Threat actors specifically target insurance brokers, senior underwriters, and claims adjusters. Because wire transfers are routine in these roles, there is ample opportunity to inject fraudulent instructions into existing, trusted payment streams without immediately raising suspicion42.

## **2\. How the Attack Works**

BEC attacks require immense patience. Threat actors do not strike immediately upon gaining access; they lurk silently in compromised inboxes for weeks, studying communication styles and financial workflows.  
Attacker  
│  
Reconnaissance (Identifying key financial personnel via LinkedIn or corporate sites)  
│  
Initial Access (Phishing, Credential Stuffing, or Adversary-in-the-Middle)  
│  
Inbox Surveillance (Silent monitoring of financial keywords: "wire", "invoice", "closing")  
│  
Persistence (Creating hidden inbox forwarding rules or malicious OAuth apps)  
│  
Interception (Identifying an ongoing high-value transaction or settlement)  
│  
Impersonation (Spoofing a vendor, executive, or broker domain)  
│  
Social Engineering (Injecting "updated" wire instructions with a manufactured urgency)  
│  
Funds Transfer (Victim wires funds to an attacker-controlled money mule account)  
│  
Business Impact (Unrecoverable financial loss once funds are moved offshore)

## **3\. Real-World History**

BEC attacks are ubiquitous across the financial and insurance sectors, though many organizations prefer to keep specific losses confidential to avoid reputational damage.

| Organization | Year | Country | Industry | Attack Method |
| :---- | :---- | :---- | :---- | :---- |
| **M\&A Insurance Broker** | N/A | UK | Insurance Broker | BEC / Invoice Fraud |
| **Children's Healthcare** | N/A | USA | Healthcare | BEC / Executive Fraud |
| **Systemic Title Fraud** | 2021+ | Global | Real Estate/Title | BEC / Escrow Fraud |

**M\&A Insurance Broker (Redscan Case Study):** A leading UK independent insurance broker fell victim to a highly targeted BEC attack. An attacker successfully phished a senior employee, gained access to their Office 365 account, and silently monitored traffic43. The attacker identified an ongoing £300,000 transaction. Using a typo-squatted domain (adding an extra, barely noticeable letter to the real domain), the attacker impersonated the broker, intercepting communications between the buyer and seller to provide fraudulent wire instructions. The attacker also set up hidden inbox rules to automatically delete legitimate incoming replies, ensuring the victim remained unaware. The attack was only foiled at the last minute because a vigilant client insisted on verbal verification over the phone42.  
**Children's Healthcare of Atlanta:** Demonstrating the devastating financial impact of executive impersonation, this pediatric care provider lost $3.6 million in a BEC scam. Attackers impersonated the Chief Financial Officer (CFO), exploiting the inherent authority of the position to bypass standard financial scrutiny and order massive wire transfers44.  
**Systemic Title and Escrow Fraud:** FBI and industry data highlight the systemic, continuous targeting of title insurance, real estate closing firms, and commercial brokers. Scammers routinely compromise the accounts of escrow agents or attorneys, providing fake wire instructions for property settlements or large commercial claims just hours before a closing38. By the time the legitimate party inquires about the missing funds, the money has already been dispersed globally by money mules.

## **4\. Why the Attack Succeeded**

BEC succeeds by brilliantly exploiting human trust and broken financial processes37. Technically, organizations fail to mandate MFA on cloud email platforms, or they fall victim to advanced Adversary-in-the-Middle (AiTM) phishing that intercepts session cookies, thereby bypassing basic MFA40. Procedurally, businesses fail to implement rigorous "out-of-band" verification for changes to wire instructions. Employees often accept updated payment details via email without verifying the change via a trusted phone number, allowing spoofed emails to override established financial controls45.

## **5\. Indicators of Compromise (IOCs)**

BEC IOCs are primarily configuration and behavioral anomalies within cloud email platforms.

| IOC Type | Indicator Value | Description |
| :---- | :---- | :---- |
| **Email Rule** | Forward to External | Hidden inbox rules forwarding emails to free services (e.g., @gmail.com, @yahoo.com)43. |
| **Email Rule** | Move to RSS/Archive | Rules designed to immediately hide incoming emails containing keywords like "wire", "fraud", or "invoice". |
| **Network** | Impossible Travel | Consecutive logins to Office 365 from geographically disparate locations (e.g., London and Lagos) within minutes. |
| **Domain** | Typo-squatting | Presence of subtly altered domains in communication logs (e.g., cornpany.com instead of company.com). |

## **6\. Detection**

Detection relies heavily on advanced Email Security Gateways (ESG) and cloud monitoring. ESGs must leverage AI and machine learning to detect behavioral anomalies, such as executives communicating from unusual IP addresses, sudden shifts in writing style, or mismatching "Reply-To" headers. SIEM and Cloud Security Posture Management (CSPM) platforms must alert immediately on the creation of sweeping email forwarding rules or the authorization of unverified, highly privileged OAuth applications within the corporate tenant (MITRE T1114 Email Collection).

## **7\. Prevention**

Preventing BEC requires an equal focus on technology and human process. Process improvements are paramount: organizations must institute mandatory, out-of-band verbal verification for *any* change to payment or wire instructions, using a known phone number from a trusted system of record, never a number provided in the suspicious email41. Technical controls must implement strict DMARC, SPF, and DKIM policies to prevent external domain spoofing. Organizations must enforce context-aware, phishing-resistant MFA (such as FIDO2) for all email accounts to defeat AiTM attacks43. Finally, user awareness programs must conduct targeted simulation training for finance, HR, and executive teams, focusing explicitly on executive impersonation and fake invoice scenarios41.

## **8\. Incident Response**

Rapid execution of the incident response plan is the only way to recover stolen funds. Identification involves quickly auditing Office 365/Workspace logs to identify the point of compromise, uncovering unauthorized forwarding rules, and determining the full scope of emails accessed or intercepted43. Containment requires a forced session kill and password reset for the compromised user. Responders must remove all malicious inbox rules and revoke suspicious OAuth tokens. Crucially, the organization must contact the receiving financial institution *immediately* to initiate a wire recall and invoke the Financial Fraud Kill Chain, as funds are typically unrecoverable within 48 hours37. Eradication involves cleansing the tenant and implementing conditional access policies restricting logins to approved geographic regions.

## **9\. Key Takeaways**

* **Main Risks:** Immediate, often unrecoverable financial depletion and the loss of critical client trust.  
* **Business Impact:** Direct monetary loss that routinely bypasses standard cyber insurance deductibles, alongside potential legal liability for negligence in handling client or escrow funds39.  
* **Detection Priorities:** Alerting on anomalous login locations, hidden inbox rules, and domain typo-squatting.  
* **Prevention Priorities:** Phishing-resistant MFA, strict DMARC enforcement, and unbreakable out-of-band financial verification processes.

═══════════════════════════════════════════════

# **Credential Stuffing and Identity-Based Attacks**

## **1\. Overview**

Credential stuffing is a highly automated attack methodology where cybercriminals utilize massive, previously acquired databases of stolen usernames and passwords to gain unauthorized access to user accounts on a target system47. These credential databases are typically compiled from previous, unrelated public breaches or harvested directly from user devices via infostealer malware.  
Attackers use this method because it exploits a fundamental and ubiquitous human failing: password reuse across multiple platforms. Armed with vast botnets and proxy networks, attackers can test millions of credential pairs against target portals in hours, yielding a statistically predictable and highly profitable rate of success without needing to breach the company's internal infrastructure48. In 2024, researchers uncovered the "Mother of all Breaches" (MOAB), an exposed dataset containing over 16 billion working credentials harvested from infostealer malware, effectively providing attackers with an industrial-scale credential buffet49.  
Insurance companies are heavily targeted because they host extensive, public-facing portals for policyholders, agents, brokers, and medical providers50. These portals contain rich troves of PII, PHI, and financial mechanisms (like wellness reward points, claims processing, and policy loans). Successfully breaching these accounts allows attackers to commit identity theft, execute insurance fraud, or act as an Initial Access Broker (IAB) by selling the authenticated sessions to ransomware syndicates50.

## **2\. How the Attack Works**

The attack is strictly volume-driven, requiring orchestration tools and proxy networks to bypass basic security measures like IP rate limiting.  
Attacker  
│  
Resource Acquisition (Purchasing combo-lists or infostealer logs on dark web)  
│  
Infrastructure Setup (Deploying residential proxy networks to distribute traffic)  
│  
Automated Execution (Bots inject credentials into the insurance login portal)  
│  
Validation (Separating successful authentications from failures)  
│  
Account Takeover (ATO) (Accessing the compromised customer/agent portal)  
│  
Privilege Exploitation (Navigating the portal to find valuable data or financial levers)  
│  
Monetization (Stealing PII, redeeming reward points, executing fraudulent claims)

## **3\. Real-World History**

The volume of credential stuffing attacks against the insurance sector has skyrocketed, resulting in significant consumer data exposure.

| Organization | Year | Country | Industry | Attack Method |
| :---- | :---- | :---- | :---- | :---- |
| **Humana** | 2018-19 | USA | Health / Life | Credential Stuffing |
| **State Farm** | 2019 | USA | Auto/Property | Credential Stuffing |
| **PracticeMax** | 2021 | USA | Billing/TPA | Lack of MFA / Credential Theft |

**Humana (2018-2019):** Healthcare giant Humana faced prolonged, aggressive credential stuffing campaigns targeting their Humana.com and Go365.com wellness portals. Attackers utilized massive combo-lists originating from foreign IP addresses to validate active credentials. Upon achieving Account Takeover (ATO), the attackers accessed PHI and fraudulently redeemed Go365 reward points for gift cards50. Furthermore, affiliated entities like Bankers Life experienced credential compromise via phishing that exposed the insurance applications of thousands of customers50.  
**State Farm (2019):** A major credential stuffing attack targeted the customer portal of State Farm. The attackers utilized automated bots to confirm valid usernames and passwords, successfully gaining access to numerous policyholder accounts. The incident underscored the severe vulnerability of consumer-facing insurance platforms to automated brute-force attacks and the necessity of proactive credential screening52.  
**PracticeMax (2021):** PracticeMax, a massive billing and practice management vendor utilized by major insurers (including Humana and Anthem), suffered a catastrophic breach originating from stolen credentials and the complete lack of MFA on their remote access systems. This initial identity compromise cascaded rapidly into a full ransomware deployment, exposing the PHI of over 165,000 patients. The vendor failed to notify affected patients in a timely manner, taking over a year in some cases, highlighting the immense downstream danger of poorly secured third-party identities55.

## **4\. Why the Attack Succeeded**

Credential stuffing succeeds fundamentally due to negligent password reuse by consumers and employees, compounded exponentially by the proliferation of infostealer malware (e.g., Lumma, Vidar, Raccoon) that constantly replenishes dark web markets with fresh, active session tokens and credentials49. On the technical side, insurance portals lacking mandatory MFA, behavioral CAPTCHAs, or robust bot mitigation solutions are entirely defenseless against distributed, low-and-slow authentication attempts rotated across thousands of residential IP addresses51.

## **5\. Indicators of Compromise (IOCs)**

IOCs for credential stuffing are predominantly derived from web authentication logs.

| IOC Type | Indicator Value | Description |
| :---- | :---- | :---- |
| **Web Log** | High Failure Ratio | An unusually high ratio of failed logins to successful logins (e.g., a 99% failure rate on the /auth endpoint). |
| **Network** | Distributed Login Sources | Thousands of login attempts originating from disparate residential IP addresses or known VPN exit nodes. |
| **Application** | Single IP / Multiple Accounts | A single IP address attempting to authenticate against hundreds of unique, unrelated user accounts. |
| **Behavioral** | Rapid Post-Login Activity | Immediate, machine-speed point redemptions, email address changes, or mass downloading of policy documents post-authentication. |

## **6\. Detection**

Detecting distributed credential stuffing requires specialized tools beyond traditional SIEM alerting. Organizations must deploy advanced Web Application Firewalls (WAF) and Bot Management platforms that evaluate browser telemetry, mouse movements, keystroke dynamics, and JavaScript execution to differentiate between human users and automated scripts. SIEMs should configure alerts for "brute force" patterns (MITRE T1110 Brute Force: Credential Stuffing), such as rapid, successive logins across disparate accounts from the same subnet. Furthermore, Threat Intelligence teams must continuously monitor dark web forums and credential leak repositories (e.g., HaveIBeenPwned) for corporate domain exposure to preempt ATO attempts32.

## **7\. Prevention**

Prevention strategies must focus on breaking the automation cycle and enforcing identity verification. Authentication controls must enforce mandatory MFA for all user portals, ideally utilizing adaptive/risk-based authentication that triggers step-up verification when a user logs in from a new device, a recognized proxy, or an anomalous geographic location16. Password hygiene programs should implement policies that actively check newly created or changed passwords against known compromised lists (aligning with NIST SP 800-63B guidelines). Finally, perimeter defenses must deploy specialized anti-bot solutions and CAPTCHAs on all public-facing authentication forms to economically disrupt automated tooling.

## **8\. Incident Response**

When a credential stuffing campaign is detected, Identification involves isolating the authentication logs to quantify the exact number of accounts successfully breached versus those merely targeted. Containment requires temporarily throttling or blocking the attacking IP subnets at the WAF level. Responders must implement forced password resets and session revocation for all successfully compromised accounts52. Eradication involves deploying enhanced WAF rules and CAPTCHAs to halt the automated traffic permanently. During Recovery, organizations must formally notify impacted customers regarding the ATO, provide credit monitoring if PII/PHI was accessed, and restore any fraudulently drained assets (e.g., stolen reward points) to maintain brand trust50.

## **9\. Key Takeaways**

* **Main Risks:** Mass Account Takeover (ATO) leading to identity theft, consumer fraud, and acting as an initial access vector for catastrophic internal network breaches.  
* **Business Impact:** Severe loss of customer trust, regulatory scrutiny regarding portal security, and direct financial costs associated with fraud remediation and litigation.  
* **Detection Priorities:** Identifying high-velocity login failures, tracking distributed authentication sources, and alerting on post-login anomalies.  
* **Prevention Priorities:** The enforcement of mandatory MFA on all portals, proactive compromised credential screening, and the deployment of robust bot mitigation software.

═══════════════════════════════════════════════

# **Conclusion: Risk Ranking and Final Analysis**

Based on exhaustive analysis of the contemporary threat landscape, financial severity, blast radius, and the unique structural vulnerabilities inherent to the insurance sector, the top five attacks are ranked from highest to lowest systemic risk as follows:

> 1. **Supply Chain and MFT Zero-Day Exploits**  
   * **Justification:** Highest systemic risk. The insurance industry relies heavily on an interconnected web of TPAs, brokers, and external vendors. A single zero-day exploit in an MFT appliance (like MOVEit) bypasses all internal defenses and exposes millions of records instantly. The blast radius is completely uncontrollable, and prevention is highly reliant on third-party security practices, making this the most dangerous threat to the sector's data integrity.  
> 2. **Multi-Extortion Ransomware**  
   * **Justification:** Highest direct financial and operational damage. Ransomware causes total operational paralysis, preventing critical functions like underwriting and claims processing. The multi-extortion model ensures that even highly resilient companies suffer massive brand damage and catastrophic regulatory fines due to the public leakage of medical and financial data.  
> 3. **API Vulnerabilities and IDOR**  
   * **Justification:** Highest risk for silent, massive data exposure. As insurers rushed through digital transformation, poorly coded APIs have provided an open door to backend customer databases. These attacks are exceptionally easy to execute, extremely difficult to detect via traditional perimeter security, and routinely result in the exposure of millions of records without triggering a single alarm.  
> 4. **Business Email Compromise (BEC) and Funds Transfer Fraud**  
   * **Justification:** Highest frequency of direct, unrecoverable monetary loss. Because the industry moves vast sums of money daily via wire transfers, BEC remains incredibly lucrative. However, it is ranked fourth because its impact, while severe financially, is usually isolated to specific transactions rather than causing systemic enterprise collapse or mass customer data exposure.  
> 5. **Credential Stuffing and Identity-Based Attacks**  
   * **Justification:** Highest volume threat. Driven by rampant password reuse and infostealer malware, this attack vector constantly hammers insurance portals. While dangerous and a leading cause of Account Takeover, the impact per individual incident is generally lower than the other threats, and the attack can be highly mitigated through the strict enforcement of modern, adaptive MFA.

The insurance industry remains a highly lucrative target for advanced threat actors. Defending against these systemic risks requires a comprehensive transition from reactive perimeter defense to proactive, zero-trust architectures, rigorous third-party risk management, and the continuous, behavioral monitoring of digital identities.

#### **Works cited**

> 1. Cybersecurity Insurance Market Report 2025-2030, by Coverage, Geo, Tech, [https://www.marketsandmarkets.com/Market-Reports/cyber-insurance-market-47709373.html](https://www.marketsandmarkets.com/Market-Reports/cyber-insurance-market-47709373.html)  
> 2. Cyber security resilience 2025 – Claims and risk management trends \- Allianz Commercial, [https://commercial.allianz.com/news-and-insights/reports/cyber-risk-trends.html](https://commercial.allianz.com/news-and-insights/reports/cyber-risk-trends.html)  
> 3. Cyber insurance: state of the art, trends and future directions \- PMC, [https://pmc.ncbi.nlm.nih.gov/articles/PMC9841933/](https://pmc.ncbi.nlm.nih.gov/articles/PMC9841933/)  
> 4. Insurers fear rise in sensitive data theft as cyber crime tops list of the sectors key concerns, [https://www.pwc.co.uk/press-room/press-releases/insurers-fear-rise-in-sensitive-data-theft-as-cyber-crime-tops-l.html](https://www.pwc.co.uk/press-room/press-releases/insurers-fear-rise-in-sensitive-data-theft-as-cyber-crime-tops-l.html)  
> 5. Starhealth Insurance Debacle: Information warfare using fabricated evidence \- CloudSEK, [https://www.cloudsek.com/blog/starhealth-insurance-debacle-information-warfare-using-fabricated-evidence](https://www.cloudsek.com/blog/starhealth-insurance-debacle-information-warfare-using-fabricated-evidence)  
> 6. Star Health Insurance Data Breach: Lessons In Cybersecurity \- Sprinto, [https://sprinto.com/blog/star-health-insurance/](https://sprinto.com/blog/star-health-insurance/)  
> 7. Avaddon Ransomware Attack Hits AXA Group \- Cyberint, [https://cyberint.com/blog/research/avaddon-ransomware-attack-hits-axa-philippines-malaysia-thailand-and-hong-kong/](https://cyberint.com/blog/research/avaddon-ransomware-attack-hits-axa-philippines-malaysia-thailand-and-hong-kong/)  
> 8. Avaddon Ransomware Threat Actor Profile \- TTPs, IOCs & History | Huntress, [https://www.huntress.com/threat-library/threat-actors/avaddon](https://www.huntress.com/threat-library/threat-actors/avaddon)  
> 9. CNA Financial Ransomware 2021: $40M Payment \- Cloudskope, [https://www.cloudskope.com/breaches/cna-financial-ransomware-2021](https://www.cloudskope.com/breaches/cna-financial-ransomware-2021)  
> 10. Reviewing 2021 Biggest Ransomware Attacks \- PDI Security & Network Solutions, [https://security.pditechnologies.com/blog/reviewing-2021s-biggest-ransomware-attacks/](https://security.pditechnologies.com/blog/reviewing-2021s-biggest-ransomware-attacks/)  
> 11. Lessons from Ransomware Payments by CNA, JBS and Colonial Pipeline, [https://www.insurancejournal.com/magazines/mag-features/2021/12/06/644276.htm](https://www.insurancejournal.com/magazines/mag-features/2021/12/06/644276.htm)  
> 12. 2021 Cyber Attacks and 7 Major Lessons Learned \- Proficio, [https://www.proficio.com/2021\_cyber\_attacks/](https://www.proficio.com/2021_cyber_attacks/)  
> 13. AXA faces Avaddon ransomware | INCIBE-CERT, [https://www.incibe.es/en/incibe-cert/publications/cybersecurity-highlights/axa-faces-avaddon-ransomware](https://www.incibe.es/en/incibe-cert/publications/cybersecurity-highlights/axa-faces-avaddon-ransomware)  
> 14. Avaddon Ransomware Hits Insurance Giant AXA \- Heimdal Security, [https://heimdalsecurity.com/blog/avaddon-ransomware-hits-insurance-giant-axa/](https://heimdalsecurity.com/blog/avaddon-ransomware-hits-insurance-giant-axa/)  
> 15. AXA Insurance Ransomware Attack hits 4 Asian Countries \- Sangfor Technologies, [https://www.sangfor.com/blog/cybersecurity/axa-insurance-ransomware-attack-hits-4-asian-countries](https://www.sangfor.com/blog/cybersecurity/axa-insurance-ransomware-attack-hits-4-asian-countries)  
> 16. What Caused the Medibank Data Breach? \- UpGuard, [https://www.upguard.com/blog/what-caused-the-medibank-data-breach](https://www.upguard.com/blog/what-caused-the-medibank-data-breach)  
> 17. A Cheater's Dilemma \- Inde Technology, [https://www.inde.nz/blog/a-cheaters-dilemma](https://www.inde.nz/blog/a-cheaters-dilemma)  
> 18. Medibank hacker exposes data \- Computer One, [https://computerone.com.au/criminals-behind-medibank-cyber-attack-exposes-thousands-of-customer-health-data/](https://computerone.com.au/criminals-behind-medibank-cyber-attack-exposes-thousands-of-customer-health-data/)  
> 19. Security Now\! \#897 \- 11-15-22 \- Memory-Safe Languages, [https://www.grc.com/sn/sn-897-notes.pdf](https://www.grc.com/sn/sn-897-notes.pdf)  
> 20. MOVEit software cyberattack notification | CSU System, [https://csusystem.edu/moveit-software-cyberattack-notification/](https://csusystem.edu/moveit-software-cyberattack-notification/)  
> 21. What we know about the MOVEit exploit and ransomware attacks | BlackFog, [https://www.blackfog.com/what-we-know-about-the-moveit-exploit/](https://www.blackfog.com/what-we-know-about-the-moveit-exploit/)  
> 22. Progress Software's MOVEit meltdown: uncovering the fallout | Cybersecurity Dive, [https://www.cybersecuritydive.com/news/progress-software-moveit-meltdown/703659/](https://www.cybersecuritydive.com/news/progress-software-moveit-meltdown/703659/)  
> 23. Case 1:23-md-03083-ADB Document 1517 Filed 07/31/25 Page 1 of 117 \- United States District Court for the District of Massachusetts, [https://www.mad.uscourts.gov/caseinfo/pdf/mdl/3083/Order%2023.pdf](https://www.mad.uscourts.gov/caseinfo/pdf/mdl/3083/Order%2023.pdf)  
> 24. Data Spill Management: A Comprehensive Guide \- Scrut, [https://www.scrut.io/post/data-spill-management](https://www.scrut.io/post/data-spill-management)  
> 25. List of Data Breaches and Cyber Attacks in 2023 \- GRC Solutions, [https://grcsolutions.io/list-of-data-breaches-and-cyber-attacks-in-2023/](https://grcsolutions.io/list-of-data-breaches-and-cyber-attacks-in-2023/)  
> 26. MOVEIT CUSTOMER DATA SECURITY BREACH LITIGATION MDL No. 3083 TR, [https://www.jpml.uscourts.gov/sites/jpml/files/MDL-3083-Transfer\_Order-9-23.pdf](https://www.jpml.uscourts.gov/sites/jpml/files/MDL-3083-Transfer_Order-9-23.pdf)  
> 27. Big names disclose MOVEit-related breaches, including PwC, EY and Genworth Financial, [https://www.cybersecuritydive.com/news/moveit-breaches-pwc-ey-genworth/653821/](https://www.cybersecuritydive.com/news/moveit-breaches-pwc-ey-genworth/653821/)  
> 28. About Accellion Security Incident \- Singapore \- Singtel, [https://www.singtel.com/personal/support/about-accellion-security-incident](https://www.singtel.com/personal/support/about-accellion-security-incident)  
> 29. What Is Insecure Direct Object Reference (IDOR)? \- SentinelOne, [https://www.sentinelone.com/cybersecurity-101/cybersecurity/insecure-direct-object-reference/](https://www.sentinelone.com/cybersecurity-101/cybersecurity/insecure-direct-object-reference/)  
> 30. SEC Investigating Data Leak at First American \- ACA Group, [https://www.acaglobal.com/industry-insights/sec-investigating-data-leak-first-american/](https://www.acaglobal.com/industry-insights/sec-investigating-data-leak-first-american/)  
> 31. First American Financial Corp Data Breach: What Happened, Impact, and Lessons, [https://www.huntress.com/threat-library/data-breach/first-american-financial-data-breach](https://www.huntress.com/threat-library/data-breach/first-american-financial-data-breach)  
> 32. First American Corporation Data Breach: What & How It Happened? \- Twingate, [https://www.twingate.com/blog/tips/First%20American%20Corporation-data-breach](https://www.twingate.com/blog/tips/First%20American%20Corporation-data-breach)  
> 33. First American Financial Admits Data Breach Major Digital Companies Against Government Eavesdropping On Chats \- Pinkerton, [https://pinkerton.com/media/our-insights/briefings/sources/cybersecurity-newsletter-6-20192.pdf](https://pinkerton.com/media/our-insights/briefings/sources/cybersecurity-newsletter-6-20192.pdf)  
> 34. SEC Charges Issuer With Cybersecurity Disclosure Controls Failures, [https://www.sec.gov/newsroom/press-releases/2021-102](https://www.sec.gov/newsroom/press-releases/2021-102)  
> 35. Star Health takes Telegram and hacker to court over massive data leak | Insurance Business, [https://www.insurancebusinessmag.com/asia/news/cyber/star-health-takes-telegram-and-hacker-to-court-over-massive-data-leak-507778.aspx](https://www.insurancebusinessmag.com/asia/news/cyber/star-health-takes-telegram-and-hacker-to-court-over-massive-data-leak-507778.aspx)  
> 36. Star Health data leak case: Madras High Court makes minor tweaks to its previous order, [https://www.thehindu.com/news/national/tamil-nadu/star-health-data-leak-case-madras-high-court-makes-minor-tweaks-to-its-previous-order/article68796884.ece](https://www.thehindu.com/news/national/tamil-nadu/star-health-data-leak-case-madras-high-court-makes-minor-tweaks-to-its-previous-order/article68796884.ece)  
> 37. Business Email Compromise: How BEC Scams Work and What Victims Can Do, [https://www.daeryunlaw.com/us/practices/detail/business-email-compromise](https://www.daeryunlaw.com/us/practices/detail/business-email-compromise)  
> 38. Federal Bureau of Investigation Business Email Compromise and Real Estate Wire Fraud 2022 \- FBI, [https://www.fbi.gov/file-repository/fy-2022-fbi-congressional-report-business-email-compromise-and-real-estate-wire-fraud-111422.pdf](https://www.fbi.gov/file-repository/fy-2022-fbi-congressional-report-business-email-compromise-and-real-estate-wire-fraud-111422.pdf)  
> 39. What is Business Email Compromise? \- IBM, [https://www.ibm.com/think/topics/business-email-compromise](https://www.ibm.com/think/topics/business-email-compromise)  
> 40. How Business Email Compromise (BEC) Drives Claims | Corvus by Travelers, [https://www.corvusinsurance.com/blog/how-business-email-compromise-drives-claims](https://www.corvusinsurance.com/blog/how-business-email-compromise-drives-claims)  
> 41. Behind the business email compromise (BEC) scam | The Hanover Insurance Group, [https://www.hanover.com/resources/tips-individuals-and-businesses/prepare-now-learn-how/behind-business-email-compromise](https://www.hanover.com/resources/tips-individuals-and-businesses/prepare-now-learn-how/behind-business-email-compromise)  
> 42. Cyber Claims Case Study: Phishing for funds \- CFC Underwriting, [https://www.cfc.com/en-gb/knowledge/resources/case-studies/uk-cyber-claims-case-studies/cyber-claims-case-study-phishing-for-funds-uk/](https://www.cfc.com/en-gb/knowledge/resources/case-studies/uk-cyber-claims-case-studies/cyber-claims-case-study-phishing-for-funds-uk/)  
> 43. Investigating a complex business email compromise attack \- Redscan, [https://www.redscan.com/case-studies/investigating-a-complex-business-email-compromise-attack/](https://www.redscan.com/case-studies/investigating-a-complex-business-email-compromise-attack/)  
> 44. 10 Real-World Business Email Compromise (BEC) Scam Examples \- Proofpoint, [https://www.proofpoint.com/us/blog/email-and-cloud-threats/10-real-world-business-email-compromise-bec-scam-examples](https://www.proofpoint.com/us/blog/email-and-cloud-threats/10-real-world-business-email-compromise-bec-scam-examples)  
> 45. Wire Transfer Fraud and Business Email Compromise (BEC) | Cowles Thompson, [https://www.cowlesthompson.com/resources/practice/business-law/wire-transfer-fraud-and-business-email-compromise-bec/](https://www.cowlesthompson.com/resources/practice/business-law/wire-transfer-fraud-and-business-email-compromise-bec/)  
> 46. Race Against the Clock to Recover $1.3M from Business Email Compromise \- Coalition, [https://www.coalitioninc.com/case-studies/education/cyber-insurance-helps-recover-funds-transfer-fraud-after-email-compromise](https://www.coalitioninc.com/case-studies/education/cyber-insurance-helps-recover-funds-transfer-fraud-after-email-compromise)  
> 47. How to navigate credential stuffing attacks? \- CAI, [https://www.cai.io/resources/thought-leadership/credential-stuffing-attack-theft](https://www.cai.io/resources/thought-leadership/credential-stuffing-attack-theft)  
> 48. DATA BREACH \- Identity Theft Resource Center | ITRC, [https://www.idtheftcenter.org/wp-content/uploads/2020/01/01.28.2020\_ITRC\_2019-End-of-Year-Data-Breach-Report\_FINAL\_Highres-Appendix.pdf](https://www.idtheftcenter.org/wp-content/uploads/2020/01/01.28.2020_ITRC_2019-End-of-Year-Data-Breach-Report_FINAL_Highres-Appendix.pdf)  
> 49. Data Breaches 2025 | Complete List & Statistics \- DeXpose, [https://www.dexpose.io/data-breaches-2025/](https://www.dexpose.io/data-breaches-2025/)  
> 50. 1 of 2 Attachment I.B.2-39 Humana PHI B, [https://finance.ky.gov/eProcurement/HumanaResponse/50\_Attachment%20I.B.2-39\_Humana%20PHI%20Breaches.pdf](https://finance.ky.gov/eProcurement/HumanaResponse/50_Attachment%20I.B.2-39_Humana%20PHI%20Breaches.pdf)  
> 51. Humana Breaches Reflect Chronic Credential Theft in Healthcare \- Dark Reading, [https://www.darkreading.com/endpoint-security/humana-breaches-reflect-chronic-credential-theft-in-healthcare](https://www.darkreading.com/endpoint-security/humana-breaches-reflect-chronic-credential-theft-in-healthcare)  
> 52. Incident Of The Week: State Farm Insurance Discloses Recent Credential Stuffing Attack, [https://www.cshub.com/attacks/articles/incident-of-the-week-state-farm-insurance-discloses-recent-credential-stuffing-attack](https://www.cshub.com/attacks/articles/incident-of-the-week-state-farm-insurance-discloses-recent-credential-stuffing-attack)  
> 53. State Farm Breach Highlights Threat of Credential Stuffing Attacks, [https://www.cutimes.com/2019/08/12/state-farm-breach-highlights-threat-of-credential-stuffing-attacks/](https://www.cutimes.com/2019/08/12/state-farm-breach-highlights-threat-of-credential-stuffing-attacks/)  
> 54. State Farm Credential Stuffing Attack \- "Bad Actor" Confirmed Information \- Kehoe Law Firm, [https://kehoelawfirm.com/state-farm-credential-stuffing/](https://kehoelawfirm.com/state-farm-credential-stuffing/)  
> 55. Dental Practice Cyber Incidents: 7 Breaches That Exposed the Industry's Blind Spots (2024–2025) \- SecurEveryone, [https://www.secureveryone.com/blog/dental-practice-cyber-incidents-2024-2025](https://www.secureveryone.com/blog/dental-practice-cyber-incidents-2024-2025)