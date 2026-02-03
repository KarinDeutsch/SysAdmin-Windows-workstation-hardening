# Backup & Recovery

This document defines a backup and recovery strategy for a Windows workstation with the goal of ensuring data availability, minimizing downtime, and enabling reliable recovery from common failure scenarios. Backups are treated as an operational requirement, not a security afterthought.

The focus is on recoverability, verification, and responsibility rather than tools or automation details.

---

## 1. Backup Philosophy

Backups exist to ensure **availability and continuity**, not just protection against ransomware.

Key principles:
- **Backups are not archives:** Backups support recovery; archives support long-term retention.
- **Recoverability over volume:** A smaller number of verified, restorable backups is preferable to large quantities of untested data.
- **Testing is mandatory:** A backup that has not been restored successfully is assumed to be unreliable.

The objective is predictable recovery under pressure.

---

## 2. Data Classification (Workstation Scope)

Data is classified to ensure backup effort is proportional to business impact.

### Critical Data
- User-created files and documents
- Application data required for daily work
- Configuration files necessary for system or application operation

Loss of this data directly impacts productivity or operations.

---

### Important Data
- System configuration and settings
- Application preferences and profiles

Loss is inconvenient but recoverable with moderate effort.

---

### Replaceable Data
- Operating system binaries
- Installed applications
- Cached or temporary files

These are excluded from routine file-level backups and restored through reinstallation or system recovery.

---

## 3. Backup Strategy

### Frequency
- **Daily backups** for critical user and application data
- **More frequent backups** for data that changes regularly or has low tolerance for loss
- **Periodic full system images** to support rapid system recovery

---

### Retention Philosophy
- Short-term retention for rapid rollback
- Longer retention for protection against delayed discovery of data loss or corruption
- Retention periods are defined by operational needs, not storage availability

---

### Storage Separation
- Backups are stored across multiple locations to prevent single points of failure
- At least one copy is isolated from the primary system to reduce ransomware impact

The commonly accepted 3-2-1 principle is used as a guideline rather than a rigid rule.

---

## 4. Recovery Scenarios

### Accidental File Deletion
- Restore individual files or folders from the most recent verified backup
- Validate integrity before returning data to production use

---

### System Corruption or Instability
- Restore system configuration or revert to a known-good image
- Preserve user data where possible to minimize disruption

---

### Full System Loss
- Rebuild the base system from installation media
- Restore user data and configurations from backups
- Validate system functionality before returning the workstation to service

Recovery procedures prioritize speed, clarity, and predictability.

---

## 5. Verification and Responsibility

### Backup Verification
- Regular restore tests confirm backup integrity
- Failed backups or restore tests are treated as operational incidents

---

### Responsibility
- Backup execution is automated where possible
- Verification and oversight remain an administrative responsibility
- Users are not responsible for ensuring backups exist or function

Clear ownership ensures backups do not silently fail.

---

## 6. Failure Handling

- Backup failures are investigated promptly
- Root causes are documented and corrected
- Backup reliability is reviewed periodically as part of routine system maintenance

Backups are only effective when failure is visible and acted upon.
