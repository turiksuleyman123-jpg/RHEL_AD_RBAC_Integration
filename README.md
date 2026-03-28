# Enterprise Linux Integration: Active Directory & RBAC with RHEL 10

This project demonstrates the integration of a **Red Hat Enterprise Linux (RHEL) 10** system into a **Windows Server 2022 Active Directory** domain. It focuses on implementing **Role-Based Access Control (RBAC)** by managing Linux `sudo` privileges through AD security groups.

## 🚀 Overview

In modern hybrid environments, centralized identity management is crucial for security and scalability. This project eliminates "identity islands" by allowing Linux servers to consume identities directly from Active Directory using **SSSD** (System Security Services Daemon) and **Kerberos**.

### Key Features
* **Centralized Authentication:** Domain users can log in via SSH using AD credentials.
* **Active Directory RBAC:** Leveraging AD Security Groups to grant `sudo` permissions without local configuration changes.
* **Identity Mapping:** Automatic UID/GID mapping for AD objects.
* **Automated Provisioning:** Automatic creation of home directories for domain users upon their first login.

## 🛠 Tech Stack
* **OS:** RHEL 10
* **Domain Controller:** Windows Server 2022
* **Tools:** `realmd`, `sssd`, `adcli`, `samba-common-tools`
* **Protocols:** Kerberos, LDAP, SMB

## 📖 Configuration Highlights

### 1. SSSD Configuration
The core of the integration lies in `/etc/sssd/sssd.conf`. It ensures seamless communication with the Domain Controller and handles ID mapping.

### 2. Sudoers Integration
Instead of manual user management, a specific AD group (e.g., `Linux_Admins`) is mapped to the sudoers policy:
```bash
# Location: /etc/sudoers.d/ad_admins
"%Linux_Admins@yourdomain.local" ALL=(ALL) ALL
