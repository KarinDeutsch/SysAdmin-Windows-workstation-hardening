# Software Management
## 1. Software Selection Philosophy
Fewer tools lead to higher stability, as each addition expands the attack surface and maintenance burden. Selection is a matter of judgment based on the following criteria: 
- **Necessity Over Novelty:** Software must meet quantifiable business outcomes or specific functional needs that existing tools cannot fulfill.
- **Risk & Security Assessment:** Evaluation includes technical maturity, data security, and vendor reputation to mitigate potential software failure or breaches.
- **Total Cost of Ownership (TCO):** Decisions weigh initial cost against long-term maintenance, support, and integration efforts.
- **Vendor Alignment:** Preference is given to vendors with roadmaps that align with organizational goals and a proven commitment to customer success. 

---

## 2. Installation Strategy
To prevent "shadow IT" and ensure system integrity, all installations follow a strictly managed process. 
- **Authorization:** Only designated IT personnel or automated deployment systems (like Microsoft Intune or Configuration Manager) can perform installs.
- **Approval Process:** Every request must go through a formal review (e.g., help desk ticket) to verify compatibility and licensing before deployment.
- **System-wide vs. User-level:**
    - System-wide (Machine): Installed in Program Files for all users. This is preferred for consistency, easier auditing, and centralized patching.
    - User-level (Profile): Installed only for a specific user. These are generally avoided as they can bypass security controls and create version fragmentation. 

---

## 3. Update & Patch Management
Stable environments require a systematic approach to patching rather than reactive updates. 
- **Controlled Deployment:** Updates are tested in a staging environment before being pushed to production to prevent system crashes or application errors.
- **The Danger of Auto-Updaters:** Uncontrolled auto-updaters are disabled by default. They risk introducing unvetted changes that can break critical integrations or create instability.
- **Failure Protocol:** Update failures must be flagged immediately for manual remediation or roll-back to maintain operational continuity.

---

## 4. Default Software Handling
A conservative approach to "debloating" ensures essential OS functions remain intact for support and compatibility. 
- **Conservative Retention:** Default applications are kept unless they present a documented security risk or functional conflict.
- **Justified Removal:** Removal is only permitted via centralized policy (e.g., Group Policy Objects) when an app is redundant or non-compliant with security standards.
- **Business Baseline:** Defaults serve as a stable starting point; customization is managed, not reckless. 

---

## 5. End-of-Life & Removal
Admins manage the lifecycle of software to prevent "software rot" and security debt. 
- **Identification:** Regular audits identify software that is no longer supported by the vendor (End-of-Life) or shows low usage metrics.
- **Risk of Lingering Software:** Outdated software is a primary target for hackers scanning for unpatched vulnerabilities.
- **Decommissioning:** Once identified as high-risk or unnecessary, software is formally retired and removed across the fleet to shrink the attack surface. 

---