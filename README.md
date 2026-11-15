# Awesome-Microsoft-Entra-Id-Backup-Recovery

# Awesome Microsoft Entra ID Backup & Recovery

> A curated list of top Microsoft Entra ID Backup and Recovery platforms — both SaaS/Hosted commercial solutions and open-source alternatives for protecting directory objects, configurations, and policies against accidental deletion, misconfiguration, and cyberattacks.
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [Druva Microsoft Entra ID Protection](#druva-microsoft-entra-id-protection)
  - [Veeam Backup for Microsoft Entra ID](#veeam-backup-for-microsoft-entra-id)
  - [Keepit for Entra ID](#keepit-for-entra-id)
  - [AvePoint Cloud Backup for Entra ID](#avepoint-cloud-backup-for-entra-id)
  - [Commvault Cloud for Entra ID](#commvault-cloud-for-entra-id)
  - [Rubrik Identity Resilience](#rubrik-identity-resilience)
  - [HYCU for Entra ID](#hycu-for-entra-id)
  - [Cayosoft Guardian](#cayosoft-guardian)
  - [Quest On Demand Recovery](#quest-on-demand-recovery)
  - [Semperis Directory Services Protector](#semperis-directory-services-protector)
- [Open-Source Software](#-open-source-software)
  - [Microsoft Graph PowerShell](#microsoft-graph-powershell)
  - [Microsoft Entra Exporter](#microsoft-entra-exporter)
  - [Microsoft 365 Desired State Configuration (DSC)](#microsoft-365-desired-state-configuration-dsc)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Microsoft Entra ID Backup and Recovery platforms. These are not open-source but are included as reference points for feature comparison.

### Druva Microsoft Entra ID Protection
**Type:** SaaS backup with granular restore and Identity Resiliency
Druva protects Microsoft Entra ID data including users, groups, roles, and applications with automated backups and granular restore capabilities [citation:13]. Key characteristics include restore from a single snapshot only (multi-snapshot restore is not supported), with ad-hoc backup jobs available from the Entra ID overview page [citation:1]. **Important consideration:** Cloud Key Management must be enabled for scheduled backups to run—without it, only manual backups are possible [citation:1]. Restoring an App registration preserves the Application ID if the object is still in the recycle bin; if permanently deleted, Microsoft creates a new app registration with a new Application ID [citation:1]. **Notable limitation:** Changes to Client Secrets or Certificates may not be captured in incremental backups due to a Microsoft Graph API limitation—updating another tracked field (like Notes or Description) forces detection [citation:1]. Identity Resiliency is available as a separate Identity workload license [citation:13]. **Best for:** Druva customers wanting Entra ID protection integrated with their broader data protection platform, accepting the Cloud Key Management prerequisite and Graph API limitations.

### Veeam Backup for Microsoft Entra ID
**Type:** Self-managed backup with item and property restore
Veeam Backup for Microsoft Entra ID is a component of Veeam Backup & Replication 12.3, deployed on a Windows-based backup server with a local or remote PostgreSQL instance for the Entra ID backup repository [citation:14]. Key restore operations include **Item restore** (users, groups, roles, administrative units, applications, conditional access policies, Intune policies) and **Properties restore** (properties of a single item at a time) [citation:2]. You can restore to the most recent state or any available restore point [citation:2]. **Important limitation:** Only the default general-purpose backup proxy can be used—deleting it disables Entra ID tenant and log backup [citation:14]. **Best for:** Organizations already using Veeam Backup & Replication wanting Entra ID protection with self-managed infrastructure and granular item restore, accepting the Windows/PostgreSQL deployment.

### Keepit for Entra ID
**Type:** Independent cloud backup with bulk restore and PIM protection
Keepit provides automated, immutable backups for Entra ID with recent enhancements including **bulk restore** for administrative units, roles, service principals, app registrations, and policies in one go [citation:3]. It now backs up **Windows LAPS** and account protection policies (local user group memberships, LAPS configurations) with an additional permission (Read device local credential passwords) [citation:3]. Recent updates added backup and restore of **Privileged Identity Management (PIM) role settings** and scheduled role activations, preserving activation rules, approval requirements, and time-bound assignments [citation:15]. It also backs up **Microsoft Intune Antivirus policies** [citation:15]. **Best for:** Organizations wanting an independent, vendor-neutral backup with strong coverage of privileged access configurations and modern Entra ID features.

### AvePoint Cloud Backup for Entra ID
**Type:** Multi-SaaS backup with flexible storage options
AvePoint provides automatic backups and retention of 100% of Entra ID data for as long as needed, with fast recovery via time-based or object-based restores [citation:4]. It explicitly notes that **Microsoft provides no native backup solution for Entra ID**, making dedicated backup essential [citation:4]. Storage options include AvePoint's scalable Azure storage or your private cloud [citation:4]. The platform is part of a broader multi-SaaS backup solution covering Microsoft 365, Azure VMs, and more [citation:4]. **Best for:** Organizations wanting Entra ID protection within a consolidated multi-SaaS backup platform with flexible data residency options.

### Commvault Cloud for Entra ID
**Type:** Unified AD + Entra ID protection with air-gap
Commvault provides automated, frequent daily backups of Entra ID data including users, groups, roles, conditional access policies, and app registrations [citation:5]. Key capabilities include **granular control** to view changes and revert them, rapid restore of deleted or modified objects, and **unified protection of hybrid AD and Entra ID** in a single solution [citation:5]. **AirGap** provides isolated, immutable storage on Azure as a last line of defense for cyber recovery [citation:5]. Commvault has been named a Leader in the Gartner Magic Quadrant for Backup and Data Protection Platforms for the 15th consecutive time [citation:5]. **Best for:** Enterprises needing unified hybrid AD + Entra ID protection with air-gapped immutable copies for cyber recovery.

### Rubrik Identity Resilience
**Type:** Orchestrated identity recovery with AD forest recovery
Rubrik provides **granular Entra ID recovery** for users, groups, roles, and conditional access policies, with the ability to roll back malicious changes and roll forward legitimate ones [citation:6]. A key differentiator is **orchestrated AD Forest Recovery** that turns Microsoft's complex manual process into a guided workflow, with AD and Entra ID stitched together as one recovery step rather than two [citation:6]. **Identity recovery runs first** during an incident so users can log back in before other M365 services are restored [citation:6]. **Best for:** Organizations needing coordinated hybrid identity recovery (AD + Entra ID) with a single orchestrated workflow and strong ransomware recovery posture.

### HYCU for Entra ID
**Type:** One-click restore with S3-compatible storage
HYCU provides automated backup and one-click restore for Entra ID tenant settings and data, including users, groups, roles and administrators, custom security attributes, conditional access policies, custom domains, administrative units, app registrations, and enterprise applications [citation:7]. Backup copies are stored in S3-compatible storage, giving control over data retention, security, and residency [citation:7]. It positions itself as protecting the "keys to the digital kingdom" given Entra ID's high change rate and attractiveness to attackers [citation:7]. **Best for:** Organizations wanting one-click restore with S3-compatible storage control and broad object coverage.

### Cayosoft Guardian
**Type:** Change monitoring with immediate rollback and forest recovery
Cayosoft Guardian continuously monitors all directory changes across on-premises, hybrid, and cloud environments, enabling **immediate rollback** of administrative mistakes or malicious changes without mounting and searching backup files [citation:8]. It recovers what native recycle bins cannot, including **object attribute data, Office 365 License Settings, Conditional Access policies, and hard-deleted objects** [citation:8]. **Immediate Active Directory Full-Forest Recovery** provides the fastest possible recovery from ransomware or wiper attacks against AD [citation:8]. Threat Detection performs real-time scans and provides remediation advice [citation:8]. **Best for:** Organizations needing continuous change monitoring with immediate rollback for Entra ID and hybrid AD, particularly for ransomware recovery scenarios.

### Quest On Demand Recovery
**Type:** Granular restore with diff reporting and hybrid dashboard
Quest On Demand Recovery provides cloud backup and restore for Entra ID objects including users, B2B users, Office 365 and Entra ID groups, applications, devices, and Cloud-only attributes for hybrid objects [citation:10]. **Diff reports** compare backups to the production Entra ID environment to identify changes or deletions, allowing selective restore of exactly what is needed rather than entire objects [citation:10]. **Bulk restore** handles multiple users, groups, attributes, and memberships without PowerShell [citation:10]. It integrates with Recovery Manager for Active Directory for a single hybrid recovery dashboard [citation:10]. Backups are encrypted and stored in Azure Storage with configurable retention [citation:10]. **Best for:** Organizations needing granular diff-based restore and a unified hybrid AD + Entra ID recovery dashboard.

### Semperis Directory Services Protector
**Type:** Real-time change auditing with automated forest recovery
Semperis DSP provides **real-time tracking and auditing** of directory changes, alongside **AD Forest Recovery (ADFR)** for automated disaster recovery orchestration [citation:9]. Related tools include Purple Knight (vulnerability assessment) and Forest Druid (attack path discovery) [citation:9]. Semperis reports that its tools have reduced downtime by up to **90%** during incidents [citation:9]. **Best for:** Organizations wanting real-time change auditing combined with automated AD forest recovery orchestration.

---

## 🟩 Open-Source Software

Self-hosted, community-driven Microsoft Entra ID Backup and Recovery approaches. The open-source ecosystem for **native Entra ID backup** is **extremely limited**—Microsoft provides no built-in backup, and dedicated open-source backup platforms do not exist. The available options are **export and configuration-as-code tools** rather than full backup/restore platforms.

### Microsoft Graph PowerShell
**Stack:** PowerShell / Microsoft Graph API | **License:** MIT (Microsoft)
Microsoft Graph PowerShell is a library for the Microsoft Graph APIs that allows you to **create custom scripts to export and import Entra ID object attributes** tailored to your organization's needs [citation:11]. It is the foundational building block for a DIY backup approach—you write scripts to read objects via Graph and write them back for restore. **Critical limitations:** This is not a backup product—it is a scripting library. You must build and maintain the export logic, restore logic, scheduling, retention, and verification yourself. There is no UI, no automated scheduling, and no support for point-in-time recovery without building it. **Best for:** Organizations with PowerShell expertise wanting full control over a custom Entra ID export/import pipeline, accepting the significant engineering effort required.

### Microsoft Entra Exporter
**Stack:** PowerShell | **License:** Open Source (Microsoft)
Microsoft Entra Exporter is a PowerShell module that **exports a local copy of certain Entra ID attributes** (users, applications, enterprise applications, roles, etc.) to a JSON file [citation:11]. It provides a more structured export than raw Graph scripting, giving you a snapshot of configuration data. **Critical limitations:** It is **export-only**—there is no built-in import or restore capability. You must write your own restore logic against the JSON output. It does not capture all Entra ID object types or attributes, and there is no scheduling or retention management. **Best for:** Organizations wanting a structured JSON export of key Entra ID objects as a starting point for a custom restore process, accepting that restore must be built separately.

### Microsoft 365 Desired State Configuration (DSC)
**Stack:** PowerShell | **License:** Open Source (Microsoft)
Microsoft 365 DSC is a PowerShell module for **declarative configuration, deployment, and management** of Microsoft 365 services, including Entra ID [citation:11]. It represents the closest open-source approach to **configuration-as-code backup**, where you define the desired state and DSC ensures the tenant matches it. **Important findings from a PoC:** When restoring a deleted user, **not all attributes are restored**—the password is replaced with a default password, and attributes pointing to non-existent objects cause non-blocking errors [citation:11]. The `Ensure` parameter controls whether an object is treated as `Present` (active) or `Absent` (disabled)—you cannot determine active/disabled state from the backup alone [citation:11]. **Critical limitations:** It is a configuration management tool, not a backup product. It does not capture the full fidelity of all object properties, does not provide point-in-time recovery, and requires significant PowerShell expertise. **Best for:** Organizations already practicing infrastructure-as-code wanting to manage Entra ID configuration declaratively, accepting that it is not a true backup/restore solution and has significant fidelity gaps.

---

## 📊 Comparison at a Glance

| Software | License | Stack | Users/Groups | Conditional Access | App Registrations | Self-Hosted | Best For |
|----------|---------|-------|--------------|---------------------|-------------------|-------------|----------|
| **Druva** | Proprietary | Cloud | ✅ | ✅ | ✅ | ❌ | Integrated data protection |
| **Veeam** | Proprietary | Windows/Postgres | ✅ | ✅ | ✅ | ✅ | Veeam ecosystem + item restore |
| **Keepit** | Proprietary | Cloud | ✅ | ✅ (PIM) | ✅ | ❌ | Independent + PIM/LAPS |
| **AvePoint** | Proprietary | Cloud | ✅ | ✅ | ✅ | (Private cloud) | Multi-SaaS consolidation |
| **Commvault** | Proprietary | Cloud | ✅ | ✅ | ✅ | (On-prem) | Hybrid AD + Entra ID + air-gap |
| **Rubrik** | Proprietary | Cloud/Appliance | ✅ | ✅ | ✅ | (Appliance) | Orchestrated AD + Entra recovery |
| **HYCU** | Proprietary | Cloud | ✅ | ✅ | ✅ | (S3 storage) | One-click restore + S3 control |
| **Cayosoft** | Proprietary | Cloud | ✅ | ✅ | ✅ | ❌ | Change monitoring + immediate rollback |
| **Quest** | Proprietary | Cloud | ✅ | ✅ | ✅ | ❌ | Diff reports + hybrid dashboard |
| **Graph PowerShell** | MIT | PowerShell | ✅ (Custom) | ✅ (Custom) | ✅ (Custom) | ✅ | Custom export/import scripts |
| **Entra Exporter** | Open Source | PowerShell | ✅ (Export) | (Export) | ✅ (Export) | ✅ | JSON export only |
| **M365 DSC** | Open Source | PowerShell | ✅ (Declarative) | ✅ (Declarative) | ✅ (Declarative) | ✅ | Configuration-as-code |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Microsoft Entra ID Backup or Recovery tool that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source.

**Note on the open-source ecosystem:** The open-source landscape for **Microsoft Entra ID backup and recovery** is **essentially nonexistent** as a turnkey solution. Microsoft explicitly provides **no native backup for Entra ID** [citation:4][citation:12], and the available open-source tools are **export and configuration-as-code utilities** rather than backup platforms. **Microsoft Graph PowerShell** requires you to build both export and restore logic from scratch [citation:11]. **Microsoft Entra Exporter** is export-only with no restore capability [citation:11]. **Microsoft 365 DSC** has significant fidelity gaps—passwords are not restored, active/disabled state cannot be determined from backups, and not all attributes are captured [citation:11]. For any production requirement to protect Entra ID with reliable restore, commercial platforms like Keepit, Rubrik, Commvault, or Quest remain the only viable options. The choice depends on whether you prioritize independent vendor-neutral storage (Keepit), hybrid AD coordination (Rubrik, Quest), air-gap cyber recovery (Commvault), or change monitoring with immediate rollback (Cayosoft).

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
