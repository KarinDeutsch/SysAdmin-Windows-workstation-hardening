# Users and Permissions
## 1. Account Types defined
### Local Administrator
**Definition:** Account with full, unrestricted control over a specific local computer. It belongs to the Administrators group that can insall software, modify system settings, and manage other user accounts.
**Purpose:** to perform system maintenance, install software, change hardware configurations, and troubleshoot
**Daily usage:** **No.** It nos not recommended to use the local Administrator for daily tasks.
**Risk Profile:** **Extremely high**. If this account is compromised, the attacker gains full control over the computer and can disable security software, install malware and more.

### Standard account
**Definition:** Account with limited privileges, designed for normal operations without the ability to make changes that affect the safety of the system
**Purpose:** for everyday tasks, including web browsing, checking emails, using office applications and play games
**Daily usage:** **Yes.** This is the recommended account type for all day-to-day work.
**Risk Profile:** **low to moderate**. If a standard user Account is compromised, the malware is generally confined to the user's personal profile and cannot infect the entire operating system. The invader could though get access to sensitive company data.

### Guest / Restricted Account
**Definition:** Built-in low-privileged account for temporary access by visitors or non-regular users that do not have a permanent profule on the computer.
**Purpose:** Allowing someone temporary access to the computer withoug needing a unique password or having their data saved permanently.
**Daily usage:** **No.** It is not suitable for regular use.
**Risk Profile:** **high**. 
**Justification for Disabeling Guest:**
- unrestricted access: it provides anonymous, unauthenticated access to the local system
- Backdoor risk: Attackers often exploit enabled guest accounts to gain initial, low-level access, from which they can attempt to escalate privileges.
- No Value: in modern, single-user scenarios, there is no need for a guest account

## 2. least Privilege Model
### Why admins do not work daily as admins
- Malware Inheritance: Programs inherit the privileges of the user running them. If an admin account is compromised by malware, that malware has full access on everything.
- Unintended Changes: Administrative accounts can make sweeping system changes. Routine tasks performed as admin risk accidental, unauthorized, or permanent damge to system configurations.
- Accountability: Using separate accounts (a standard account for daily work and a separate admin account for changes) ensures that all administrative actions are properly logged and attributable to a specific, authenticated session.

### How elevation is handled conceptually
Elevation is the process of temporarily upgrading a user's privileges for a specific, authorized action. It is conceptually managed by: 
- Separation of Duties: The user logs in with a standard, low-privilege token. Only when a task requiring higher privilege is initiated is the elevated token created.
- Context-Aware Authorization: Modern systems use techniques like User Account Control (UAC) to ask for authorization (consent) or re-authentication (credentials) before elevating privileges.
- Just-in-Time Access (JIT): Privileges are granted only for the duration of the task and automatically revoked afterwards.
- Token Filtering: Even if an administrator logs in, their full token is filtered to a standard user state until they explicitly choose to "Run as administrator". 

### What happens if credentials are compromised
If administrative credentials are stolen, the consequences are usually catastrophic: 
- Immediate System Control: The attacker gains the ability to install rootkits, modify system configurations, and bypass security controls, including antivirus.
- Lateral Movement and Persistence: Attackers can move freely across the network to access sensitive data, servers, and domain controllers. They often create backdoor accounts to maintain access even if the original credentials are changed.
- Data Breach/Ransomware: Attackers can encrypt files, delete backups, or exfiltrate sensitive data, leading to ransomware or data breaches.
- Evasion of Detection: Attackers can modify audit logs to hide their activities, making it difficult to detect the intrusion. 

In summary, not using admin privileges for daily work acts as a container; if a breach occurs, it remains isolated rather than taking down the entire system. 

## 3. Password & Authentication Policy
### Passowrd complexity philosophy
Modern security philosophy, particularly according to NIST guidelines, has shifted away from arbitrary character requirements (e.g., must have a symbol, must have a capital letter) toward length and unpredictability. 
- Length over Complexity: A longer password (or passphrase) is exponentially harder to crack than a shorter, complex one.
- Unpredictability & Randomness: The goal is to eliminate common substitutions (e.g., "P@ssword1!") and dictionary words.
- Passphrases: Using a long phrase or a string of random words (e.g., "CorrectHorseBatteryStaple") is considered superior to short, complex characters because it is easy for humans to remember but difficult for machines to guess.
- Uniqueness: Every account must have a unique password to prevent credential stuffing. 

### Lockout behavior
Lockout policies are designed to thwart brute-force attacks by limiting the number of consecutive failed login attempts. 
- Threshold & Duration: A standard policy often allows 5–10 attempts before locking the account for 15–30 minutes.
- Smart Lockout (Microsoft Entra ID): Microsoft utilizes "smart lockout," which distinguishes between logins from familiar locations (likely a user making a mistake) and unfamiliar locations (potentially an attacker).
- Risk of Denial of Service (DoS): If the lockout threshold is too low, an attacker can intentionally trigger it to lock legitimate users out, creating a DoS situation.
- Best Practice: The best practice is to set a threshold that prevents automated attacks but allows human error, often combined with Multi-Factor Authentication (MFA) to make passwords less critical. 

### Local vs Microsoft account Stance
The choice between a local account and a Microsoft account involves a tradeoff between privacy/control and convenience/security. 

### Microsoft Account (Modern Default):
- Stance: Cloud-synced, integrated with Microsoft services (OneDrive, Store), enables password-less logins (Windows Hello/PIN), and supports enhanced security features like MFA.
- Pros: Better security through account recovery options, easier recovery if a password is lost.
- Cons: Potential privacy issues (telemetry), reliance on an active internet connection, susceptibility to online, remote attacks.

### Local Account (Traditional):
- Stance: Device-specific, offline-first, credentials stored only on the local machine.
- Pros: Superior privacy, works entirely offline, no risk of external account compromise or service outages.
- Cons: No data syncing, no easy recovery (losing the password/hint can mean losing data), fewer modern security features.

### Recommendation: 
For high-security or strict privacy needs, local accounts are preferred. For convenience, integration, and easy recovery, Microsoft accounts are recommended. 

## 4. FIle & Resource Permissions
### How User Data is Separated
Data segregation ensures that one customer (tenant) cannot view or influence another customer's data. 

- Logical Isolation: Data is stored in separated logical partitions. Even if sharing a server, each customer's data is tagged with a unique Tenant ID, ensuring queries only retrieve authorized records.

- Database Schema Separation: Some platforms assign a separate database schema per tenant, providing stronger security and more flexibility in data structure.

- Encryption Keys: Data is often encrypted at rest and in transit using per-customer or per-object keys. This provides a "defense-in-depth" layer, meaning even if data boundaries are breached, the data cannot be decrypted without the correct key.

- Network Separation: Software Defined Networks (SDN) allow multiple customers to have separate networks with overlapping IP addresses without interfering with each other. 

### What Admins can Access
Tenant administrators have high-level access to manage the organization's environment but are restricted to their own "tenant" (company). 

- User Management: Admins can create, suspend, edit, and delete user accounts, as well as assign roles (e.g., RBAC).

- Data Access & Export: Admins can typically view user profiles, application usage reports, and audit logs to track activity, such as document edits.

- Security & Policy Configuration: Admins configure security settings, including enabling Multi-Factor Authentication (MFA), password policies, and restricting login access.

- Data Ownership: Admins can often transfer ownership of files and folders (e.g., in Google Workspace) and manage data retention policies, such as those in Legal Hold. 

### What Users Cannot Touch
Standard users are restricted by role-based access control (RBAC), which limits their actions to only what is necessary for their role. 

- Administrative Settings: Users cannot change global system settings, modify security policies, or alter the organization's billing information.

- Other Users' Data: Users generally cannot access or modify the personal files, emails, or data of other employees, unless explicitly shared.

- System-Level Configuration: Users cannot access raw database schemas, change network configurations, or access audit logs.

- Application Infrastructure: Users cannot modify the underlying application code, install prohibited plugins, or change the technical infrastructure of the SaaS platform. 

## 5. Edge Cases
In an emergency "something broke" scenario involving temporary contractors, organizations must balance speed with security to prevent "privilege creep" and unauthorized changes.

### 1. Just-in-Time (JIT) Access
JIT access provides temporary elevated privileges only when needed for a specific task. 
Duration-Based: Grant access for a fixed window (e.g., 2–4 hours) that automatically expires, removing the risk of forgotten standing privileges.
Task-Specific: Narrowly scope access to the specific system or resource that is broken, rather than granting broad administrative rights. 

### 2. Emergency "Break-Glass" Protocols
For critical outages, a predefined "break-glass" procedure ensures contractors can act immediately while maintaining accountability. 
Predefined Roles: Create emergency accounts or roles with the necessary permissions that remain inactive until a crisis occurs.
Accelerated Approval: Use automated workflows in ITSM tools like Jira Service Management to trigger instant approval based on an emergency ticket. 

### 3. Monitoring and Accountability
Every action taken during an emergency session must be documented for later audit. 
Session Recording: Use PAM tools like CyberArk or ScreenConnect to record the entire remote session for forensic review.
Mandatory Justification: Require contractors to provide a business reason or ticket number before the temporary access is activated. 

### 4. Zero Standing Privilege (ZSP) 
Ideally, contractors should have zero permanent privileges. 
Credential Vaulting: Store administrative credentials in a secure vault like Keeper. Contractors "check out" credentials, which are automatically rotated once the session ends.
MFA Enforcement: Multi-factor authentication is mandatory at the point of elevation, ensuring the person using the temporary admin rights is indeed the authorized contractor. 
