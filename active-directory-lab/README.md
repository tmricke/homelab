# Active Directory Domain Services Homelab

## Overview

This project documents the setup of a basic **Active Directory Domain Services (AD DS)** environment using **Windows Server 2022** running as a virtual machine in **Oracle VirtualBox**.

The purpose of this lab is to build hands-on experience with Windows Server administration and Active Directory. This stage covers installing the AD DS server role and beginning the promotion of the server to the first domain controller in a new Active Directory forest.

> **Lab status:** AD DS role installed. Server promotion to a domain controller and creation of the `lab.local` forest are in progress.

## Lab Environment

| Component | Configuration |
|---|---|
| Hypervisor | Oracle VirtualBox |
| Server OS | Windows Server 2022 Standard Evaluation |
| Server Name | `DC01` |
| Server IP | `192.168.10.10` |
| Server Role | Active Directory Domain Services |
| Planned Forest / Domain | `lab.local` |
| DNS | DNS Server installed/configured as part of domain controller promotion |

## Objectives

- Deploy a Windows Server 2022 virtual machine in VirtualBox.
- Configure the server as `DC01` with a static IP address.
- Install the Active Directory Domain Services role.
- Promote `DC01` to a domain controller.
- Create a new Active Directory forest named `lab.local`.
- Configure the Directory Services Restore Mode (DSRM) password.
- Build a foundation for later labs involving DNS, DHCP, users, groups, organizational units, permissions, Group Policy, and Windows client domain joins.

## 1. Open Server Manager

I began in **Server Manager** on the Windows Server 2022 VM. The server had already been named `DC01` and configured with the lab network settings.

![Server Manager Dashboard](images/01-server-manager-dashboard.png)

From Server Manager, I selected **Add roles and features** to begin installing Active Directory Domain Services.

## 2. Select the Destination Server

I selected `DC01` from the server pool as the destination server. Server Manager showed the server using IP address `192.168.10.10` and Windows Server 2022 Standard Evaluation.

![Select DC01 as Destination Server](images/03-select-destination-server.png)

## 3. Select Active Directory Domain Services

Under **Server Roles**, I selected **Active Directory Domain Services**. AD DS stores information about domain users, computers, groups, and other network objects and provides centralized authentication and administration.

![Select Active Directory Domain Services](images/04-select-ad-ds-role.png)

## 4. Complete the AD DS Role Installation

After installation, **AD DS** appeared in Server Manager.

![AD DS Installed](images/05-ad-ds-installed.png)

Installing the role does **not** automatically make the server a domain controller. Server Manager displayed a post-deployment notification indicating that additional configuration was required.

## 5. Begin Domain Controller Promotion

From the Server Manager notification flag, I selected **Promote this server to a domain controller**.

![Promote Server to Domain Controller](images/06-promote-domain-controller.png)

## 6. Create a New Forest

Because this is a brand-new Active Directory environment, I selected **Add a new forest** and entered:

```text
lab.local
```

![Create lab.local Forest](images/08-new-forest-lab-local.png)

For this homelab, `lab.local` provides a simple private namespace for practicing Active Directory administration.

## Domain Controller Options

The next stage uses the following lab configuration:

- **Forest functional level:** Default supported level
- **Domain functional level:** Default supported level
- **DNS Server:** Enabled
- **Global Catalog (GC):** Enabled
- **Directory Services Restore Mode (DSRM):** Password configured and stored securely

The actual DSRM password is intentionally **not documented in this public repository**.

## Verification Plan

After promotion and reboot, I will verify the deployment with:

```powershell
ipconfig /all
nslookup lab.local
Get-ADDomain
Get-ADForest
```

I will also confirm that **Active Directory Users and Computers** and **DNS Manager** open successfully and that the expected `lab.local` domain structure is present.

## What I Learned

- Installing AD DS does not by itself make a Windows Server a domain controller.
- The server must be promoted after the AD DS role and management tools are installed.
- The first domain controller creates a new **forest** and **domain**.
- DNS is tightly integrated with Active Directory.
- Domain controllers should use predictable network configuration, including a static IP address.
- Recovery credentials such as the DSRM password should not be stored in public documentation.

## Next Steps

- Complete the `lab.local` domain controller promotion.
- Verify Active Directory and DNS health.
- Create Organizational Units (OUs).
- Create test users and security groups.
- Configure group membership and permissions.
- Install and configure DHCP.
- Join Windows 10/11 client VMs to the domain.
- Create and test Group Policy Objects (GPOs).
- Practice common Active Directory troubleshooting scenarios.

## Skills Demonstrated

`Windows Server 2022` · `Active Directory Domain Services` · `DNS` · `VirtualBox` · `Windows Administration` · `Domain Controllers` · `PowerShell` · `Technical Documentation`

---

### Project Note

This repository documents a personal homelab used for learning and skills development. It is not intended to represent a production enterprise deployment.
