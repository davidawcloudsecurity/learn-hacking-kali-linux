# MITRE ATT&CK Framework Overview

The MITRE ATT&CK framework is a comprehensive knowledge base that maps adversary behavior and tactics used during real-world cyberattacks. It helps organizations understand how attackers operate, from initial access to data exfiltration. The framework is built around different stages of an attack, called **Tactics**, and the specific techniques attackers use to achieve their goals, called **Techniques**.

The framework is useful for detection, analysis, threat intelligence, and security operations. It’s divided into multiple phases, each focusing on different stages of an attack lifecycle.

## MITRE ATT&CK Framework Structure

1. **Tactics:**
   - High-level goals or objectives that attackers aim to achieve. Each tactic represents a different stage of the attack lifecycle.
   - Common tactics include:
     - **Reconnaissance (TA0043):** Gathering information to identify targets.
     - **Initial Access (TA0001):** Methods for gaining initial access to a system.
     - **Execution (TA0002):** Techniques used to execute code on a system.
     - **Persistence (TA0003):** Methods for maintaining a foothold in a target system.
     - **Privilege Escalation (TA0004):** Gaining higher-level access to systems.
     - **Defense Evasion (TA0005):** Avoiding detection and bypassing security mechanisms.
     - **Credential Access (TA0006):** Stealing credentials for further exploitation.
     - **Discovery (TA0007):** Techniques for gathering information about the environment.
     - **Lateral Movement (TA0008):** Moving across networks or systems.
     - **Collection (TA0009):** Gathering data of interest to the attacker.
     - **Exfiltration (TA0010):** Extracting data from the network or system.
     - **Impact (TA0011):** Disrupting, corrupting, or destroying systems or data.

2. **Techniques:**
   - The specific methods or tools used by adversaries to achieve their objectives in each tactic.
   - For example, under **Reconnaissance**, techniques can include searching for open ports or social engineering.

## Reconnaissance and Enumeration in MITRE ATT&CK

### **Reconnaissance (TA0043)**

This is the phase where attackers gather information about the target environment, systems, users, and vulnerabilities. The goal is to identify weaknesses that can be exploited later in the attack.

**Common Techniques in Reconnaissance:**
- **Active Scanning (T1595):** Techniques for scanning target networks or systems to identify vulnerabilities or open services.
- **Search Open Websites / Forums (T1593):** Gathering information from websites, forums, and other publicly available sources.
- **Gather Victim Identity Information (T1589):** Collecting personal or organizational information.
- **Network Sniffing (T1040):** Capturing packets from the network to gather information about the network traffic, connected devices, or protocols in use.

**Purpose of Reconnaissance:**
- Identify weaknesses in the target’s defenses.
- Collect publicly available data about the organization (e.g., names, email addresses, domain names).
- Find vulnerabilities (e.g., open ports or outdated services).

---

### **Enumeration (Discovery Phase)**

While **Reconnaissance** is about gathering information from open sources, **Enumeration** involves deeper exploration within a network or system to identify specific details. This phase is more about identifying exploitable assets and weaknesses.

**Common Techniques in Enumeration (Discovery Tactic):**
- **System Information Discovery (T1082):** Identifying system properties, software configurations, and hardware information.
- **Network Share Discovery (T1135):** Identifying shared network resources (e.g., SMB shares).
- **User Account Discovery (T1087):** Identifying user accounts in the environment.
- **File and Directory Discovery (T1083):** Searching file systems for sensitive or useful data.
- **Remote System Discovery (T1018):** Discovering remote systems within a network.

**Purpose of Enumeration:**
- Identify specific systems, users, or files that may be of interest for further exploitation.
- Map the network and determine the optimal path for lateral movement.
- Discover potential vulnerabilities or misconfigurations that can be leveraged later.

---

## How These Phases Fit into the Overall Attack Lifecycle

1. **Reconnaissance (TA0043)** – Attackers typically start here, looking for publicly available information on the target organization (e.g., through OSINT like LinkedIn, websites, or social media).
2. **Initial Access (TA0001)** – Once attackers have enough information, they attempt to gain access to a system or network.
3. **Execution and Persistence (TA0002 & TA0003)** – After gaining access, attackers execute malicious code to maintain access.
4. **Discovery and Enumeration (TA0007)** – Attackers explore the network to identify systems, users, or services to exploit.
5. **Exfiltration and Impact (TA0010 & TA0011)** – Attackers exfiltrate valuable data or initiate destructive actions.

---

## MITRE ATT&CK for Defensive Strategies

By understanding the techniques used in each stage (including Reconnaissance and Enumeration), organizations can develop defensive strategies such as:
- **Detecting reconnaissance activity** (e.g., monitoring for unusual scanning behavior).
- **Harden your environment** (e.g., reducing information exposed online, limiting network discovery).
- **Setting up traps and decoys** (e.g., honeypots to catch attackers during enumeration).
- **Using network segmentation** to limit lateral movement opportunities.

---

## Example: Detecting Reconnaissance and Enumeration

1. **Reconnaissance Detection:**
   - Monitor external IP addresses for scanning activity or unusual port sweeps.
   - Check for domain or IP addresses that are frequently searched or visited by external sources.
   - Use threat intelligence to detect known indicators of compromise (IoCs) related to recon activities.

2. **Enumeration Detection:**
   - Monitor login attempts and user account discovery, especially for unused or elevated accounts.
   - Use network monitoring to identify suspicious or abnormal network scans (e.g., SMB or DNS lookups).
   - Implement endpoint detection and response (EDR) to spot suspicious system information queries.

---

In summary, the MITRE ATT&CK framework provides a detailed, actionable view of an attacker’s techniques across multiple stages of an attack. Reconnaissance and Enumeration represent early phases in this lifecycle where attackers gather and explore information about the target before moving to more exploitative tactics. Security teams can use this framework to guide defensive strategies and improve detection and response efforts.
## My Understanding
### Recon
- [ ] What type of server is it running on. LAMP or MERN
- [ ] What type of database is it running on. SQL (e.g. MySQL or MSSQL) or NOSQL (e.g MongoDB or PostgresSQL)
- [ ] Version of OS or application
### Enumerate
- [ ] Path, folders or directory to explore
