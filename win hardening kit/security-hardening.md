# Security Hardening (Baseline)

This document describes a baseline security hardening approach for a Windows 11 workstation. The focus is on risk reduction through sensible defaults, layered protections, and operational discipline rather than extreme or high-maintenance security controls. The goal is to reduce common attack vectors while preserving system usability and maintainability.

---

## 1. Security Philosophy

Security hardening follows a **defense-in-depth** approach, where multiple overlapping controls are used so that the failure of a single mechanism does not result in full system compromise.

Key principles:
- **Risk-based security:** Not all threats are equal; controls prioritize common and high-impact attack vectors.
- **Usability matters:** Security controls must not impede daily work to the point where users attempt to bypass them.
- **Defaults first:** Built-in operating system protections are preferred unless there is a clear, documented reason to change them.

Absolute security is neither achievable nor desirable on a general-purpose workstation.

---

## 2. Account and Access Protections

User identity is a primary attack vector on modern systems.

- **Least privilege enforcement:**  
  Users operate under standard accounts for daily activities. Administrative privileges are used only when required and only for the duration of the task.

- **Credential exposure reduction:**  
  Administrative credentials are not used for routine browsing, email, or document handling, reducing exposure to phishing and malware.

- **Account safeguards:**  
  Account lockout mechanisms and User Account Control (UAC) provide friction against brute-force attempts and accidental elevation.

Separating administrative and daily-use accounts limits the impact of credential compromise and restricts attacker movement.

---

## 3. Endpoint Protection

Endpoint protection relies primarily on built-in Windows security mechanisms.

- **Built-in protection stance:**  
  Microsoft Defender is used in active mode to provide real-time protection, behavioral monitoring, and cloud-assisted threat intelligence.

- **Third-party antivirus considerations:**  
  Additional security software is not automatically superior and may increase complexity, cost, and system instability. Built-in tools are preferred unless specific organizational requirements justify alternatives.

- **Behavioral focus:**  
  Modern threats often bypass signature-based detection. Behavioral monitoring helps identify suspicious activity even when malware is previously unknown.

Security tools are kept enabled, updated, and minimally customized to avoid weakening protections.

---

## 4. Network Protections (Workstation Scope)

Network controls limit exposure to unsolicited or malicious traffic.

- **Host-based firewall usage:**  
  The Windows Defender Firewall is enabled on all network profiles (Domain, Private, Public).

- **Inbound vs outbound philosophy:**  
  Inbound connections are restricted by default, while outbound traffic is allowed unless specific risks are identified.

- **Remote access stance:**  
  Remote access to the workstation is disabled unless explicitly required. When enabled, it must be authenticated, encrypted, and limited in scope.

Network security focuses on reducing attack surface rather than attempting to filter all traffic.

---

## 5. Attack Surface Reduction

Reducing attack surface minimizes the number of exploitable components.

- **Service minimization:**  
  Unused services and features are disabled where safe to do so, reducing potential entry points.

- **Macro and script risk awareness:**  
  Office macros, scripts, and embedded content are recognized as common infection vectors. Controls prioritize preventing untrusted or unexpected execution.

- **Conservative configuration:**  
  Aggressive system tweaking is avoided. Default configurations are often more stable and predictable than heavily customized setups.

Attack surface reduction emphasizes stability and predictability over aggressive hardening.

---

## 6. Incident Awareness

Baseline hardening includes awareness, not full incident response.

- **Detection indicators:**  
  Unexpected system behavior, authentication prompts, performance degradation, or security alerts are treated as potential warning signs.

- **Escalation threshold:**  
  Suspicious activity is escalated to administrative review rather than ignored or handled informally.

- **Early visibility:**  
  Early detection reduces recovery time and limits damage, even when full prevention is not possible.

Formal incident response planning is addressed separately from baseline hardening.

---
