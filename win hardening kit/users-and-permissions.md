# Users and Permissions

## 1. Account Types Defined

### Local Administrator Account
**Definition:**  
A local account that is a member of the Administrators group, with full control over the system. It can install software, modify system-wide settings, manage users, and override file permissions.

**Purpose:**  
Used exclusively for system administration tasks such as software installation, configuration changes, troubleshooting, and maintenance.

**Daily Usage:**  
**No.** This account is not used for routine work.

**Risk Profile:**  
**Extremely high.** If compromised, an attacker gains full control of the system, including the ability to disable security controls, establish persistence, and access all user data.

---

### Standard User Account
**Definition:**  
A limited-privilege account intended for normal day-to-day operations without the ability to modify system-wide settings.

**Purpose:**  
Used for everyday tasks such as web browsing, email, office applications, and approved business software.

**Daily Usage:**  
**Yes.** This is the primary account used during normal operation.

**Risk Profile:**  
**Low to moderate.** If compromised, malicious activity is generally confined to the user profile and cannot directly modify system configuration or security settings.

---

### Guest / Restricted Account
**Definition:**  
A built-in low-privilege account intended for temporary or anonymous access.

**Stance:**  
**Disabled.**

**Justification for Disabling Guest:**
- Provides anonymous access with no accountability
- Can be abused as an initial foothold for privilege escalation
- Offers no practical value in modern workstation environments
- Temporary access is better handled with explicitly created, time-limited standard accounts

---

## 2. Least Privilege Model

### Why Administrative Accounts Are Not Used Daily
- **Privilege Inheritance:** Applications inherit the permissions of the user running them. Malware executed under an admin account gains full system access.
- **Accidental Damage:** Routine actions performed with elevated privileges increase the risk of unintended system-wide changes.
- **Containment:** Running daily tasks as a standard user limits the impact of compromise and prevents full system takeover.

---

### How Privilege Elevation Is Handled Conceptually
- **Separation of Roles:** Users authenticate with a standard account and elevate only when required.
- **User Account Control (UAC):** Elevation requires explicit consent or credential re-entry before administrative actions are performed.
- **Filtered Tokens:** Even administrators operate with a standard token until elevation is explicitly requested.
- **Just-in-Time Access:** Elevated privileges exist only for the duration of the task and are not persistent.

---

### Impact of Credential Compromise
- **Standard User Compromise:**  
  Damage is generally limited to user files and user-level persistence mechanisms.
- **Administrator Compromise:**  
  Results in full system control, potential security bypass, credential harvesting, and long-term persistence.

The separation of accounts acts as a containment boundary that significantly reduces blast radius during an incident.

---

## 3. Password and Authentication Policy

### Password Philosophy
- **Length Over Complexity:** Long passphrases are favored over short, complex passwords.
- **Unpredictability:** Avoid dictionary substitutions and reused patterns.
- **Uniqueness:** Each account uses a unique credential to prevent credential reuse attacks.
- **Human Factors:** Passwords must be memorable enough to avoid insecure storage practices.

---

### Lockout Behavior
- **Purpose:** Prevent automated brute-force attacks while allowing reasonable user error.
- **Balanced Thresholds:** Lockout thresholds are set to deter automation without enabling denial-of-service attacks.
- **Defense-in-Depth:** Password policies are ideally combined with additional authentication factors where available.

---

### Local vs Microsoft Account Stance
- **Local Accounts:**  
  Preferred for environments prioritizing privacy, offline access, and minimal cloud dependency.
- **Microsoft Accounts:**  
  Acceptable where convenience, recovery options, and modern authentication features are required.

The choice depends on organizational policy, risk tolerance, and operational needs.

---

## 4. File and Resource Permissions (Workstation Scope)

### User Data Separation
- Each user account has an isolated profile directory.
- Users cannot access or modify other users’ private data by default.
- Application data is stored within user or system contexts according to privilege level.

---

### Administrative Access Boundaries
- Administrators can access system directories and user profiles when required.
- Administrative access is used only for maintenance, recovery, or troubleshooting.
- Routine file access does not require elevated privileges.

---

### User Restrictions
Standard users are prevented from:
- Modifying system directories and registry hives
- Installing system-wide software
- Changing security configurations
- Accessing other users’ private data

These restrictions reduce attack surface and prevent unauthorized system changes.

---

## 5. Edge Cases and Exceptions

### Temporary Users
- Created as standard accounts
- Limited in scope and duration
- Removed immediately after access is no longer required

---

### Contractors
- Provided standard accounts with only required access
- No standing administrative privileges
- Access reviewed and revoked upon task completion

---

### “Something Broke” Scenario
- Administrative access is granted only for the specific task
- Elevation is temporary and documented
- Changes are reviewed after resolution to prevent privilege creep

A disciplined exception process prevents emergencies from becoming permanent security risks.
