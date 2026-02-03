# System Baseline
## 1. Initial System State
- Windows Edition: Windows 11 Pro 64bit, English
- Installation Source: ISO from Microsoft
- VMware: Workstation 17 Pro
### VMware Configuration
- Configuration Type: typical (ensures fast, straightforward setup)
- Disk Size 64GB
- Memory: 4GB
- Processors 2

---

### Installation details
- Location: USA, Keyboard US
- setting up for personal use

---

## 2. Update Strategy
### Updates
Updates are scheduled monthly and according to the Patch Tuesday (second Tuesday of the month) and done at off hours to eliminate down time. The monthly update checklist includes:
- monthly Patch: apply the monthly Patch and if needed manual Patches
- reboot: Ensure the machines restart to complete the installation
- monitor Backups: Be sure all automated backups are working properly
- check security: ensure an update of antivirus and firewall and review the settings
- free disk Space: clear temporary files to ensure enough space for updates and running

Use Windows Active hours to ensure the updates are not happening during work hours.

---

### Backups
critical data should be backed up daily at least or automatically upload changes to the cloud or server as it is changed. This way nothing is lost if anything happens. A disk image should be done about every 4 months, which creates a full copy of the system.

---

### Why this strategy
Updates can take a lot of time, and this long waiting time can cause service disruptions or productivity loss. At the same time these Patches are important especially since some of the updates are security patches. Doing those off hours keeps the security up to date without slowing down business hours. Additionally, the updates and review of the Firewall and Antivirus help the company to be up to date on the company's safety. This strategy reflects a small-to-mid-size business workstation not managed by centralized WSUS or SCCM.

---

## 3. Core System Configuration Decisions
### Telemetry & privacy stance
Telemetry is minimized to the lowest level compatible with system stability and security update delivery.
- Restricted (Disabled): All "phoning home" functionality, including usage analytics, automated crash reporting, and personalized advertising IDs. Sending of diagnostic data is minimized to ensure maximum privacy.
- Allowed (Minimal): Only essential, non-PII (Personally Identifiable Information) data required for core functionality, such as security updates or validation checks, are permitted.
- Tradeoff: By restricting telemetry, developers may lack data to improve the software or detect bugs, which could lead to a less refined user experience or longer times to patch stability issues. 

---

### Default Services
The philosophy is "Disable Unused Features," treating every enabled service as a potential security risk or resource drain. 
- Disabled (Unnecessary): Services that serve no purpose for modern, standalone, or office-based machines. Examples include fax services, Xbox Live services (if not gaming), and Printer Spooler (disabled unless needed).
- Disabled (Privacy/Security): Unnecessary cloud integrations, such as OneDrive (unless intended), telemetric background services (e.g., Connected User Experiences), and remote assistance services.
- Allowed (Essential): Security services (Firewall, Defender), critical OS networking (DNS, DHCP), and core hardware management (Bluetooth, Power Management).
- Tradeoff: Disabling services can sometimes cause dependencies to break if not done carefully. However, it frees up system resources (RAM/CPU), resulting in faster boot times and better performance. 

---

### Networking Assumptions
Networking decisions are based on the "Zero Trust" model, where no network (even home) is inherently safe, requiring verification of every connection. 
- Home Use: Assume the router is the perimeter. Secure the network by separating IoT devices (smart TVs, printers) from workstations via VLANs or guest networks. Use VPNs for public, untrusted Wi-Fi.
- Business Use: Assume a hostile environment. Use strict firewall rules, disabled, and managed endpoint protection (EDR). Remote access must always use a VPN or Zero Trust Network Access (ZTNA).
- Mobile Use: Prefer cellular data over public Wi-Fi due to superior encryption, but use a VPN if Wi-Fi is necessary. Enable full-disk encryption and strict lock-screen policies.
- Tradeoff: Increased network security (e.g., rigid firewalls) can hinder convenience, making it harder to connect to shared devices or access certain services, requiring more active management by the user. 

---

### Summary
Area        |   Decision                                            |   Primary Goal
Telemetry   |   Disable all user tracking & analytics               |   Privacy (Data Minimization)
Services    |   Disable non-essential services & startup items      |   Performance & Reduced Attack Surface
Network	    |   Implement "Never Trust, Always Verify" (Zero Trust) |   Security

---

## 4. Baseline Principles
A serious Baseline prioritizes Stability and security over the latest features. This way the company reduces technical debt and operational risk.

- Stability over experimentation: proven LTS versions of software and firmware over experimental features reducing unpredictable outages.
- Minimal installed components: remove all non-essential services, libraries and tools. Less tools mean less attack surface and simplify future patching & maintenance.
- Predictable Behavior over Aggressive Optimization: rather go for configurations that provide consistent performance rather than squeezing out marginal game through brittle tuning.

---