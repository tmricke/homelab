# Active Directory Domain Services Homelab

This lab follows the progression from a Windows Server 2022 domain controller environment to user administration, security groups, and client domain joins in `lab.local`, using Oracle VirtualBox.

## Read the Lab in Order

| Order | Lab stage | Documented work |
|---|---|---|
| 1 | [Windows Server and AD DS Setup](server-setup/README.md) | Server configuration context, AD DS installation, and beginning domain controller promotion |
| 2 | [User Creation and Verification](user-creation/README.md) | Alice Johnson, Bob Martinez, and Chris Walker in the Denver Users OU; ADUC and PowerShell verification |
| 3 | [Security Groups and Membership](security-groups/README.md) | Centralized `_Groups` OU; Helpdesk, Accounting, and ITSupport; Alice's Helpdesk membership |
| 4 | [Client Domain Joins and Troubleshooting](client-domain-join/README.md) | CLIENT01 and CLIENT02 joins, domain sign-in verification, computer OU placement, and DNS troubleshooting |

Start with **Part 1**, then follow the next-page links. Each stage has its own README and supporting screenshots so the lab stays easy to browse as it grows.

## Current Status

- The `lab.local` domain is available, and three Denver user accounts have been created and verified.
- `_Groups` is at the domain root and contains Helpdesk, Accounting, and ITSupport.
- Helpdesk is verified as a Global Security group, with Alice Johnson as a member.
- Accounting and ITSupport are confirmed as security groups; their scope is not shown in the available screenshot.
- CLIENT01 is joined, with Alice's domain sign-in and Workstations OU placement verified. CLIENT02's join was reported successful and its AD computer account located; final OU placement and domain-user sign-in screenshots remain to be captured.
- Resource permissions and effective-access testing remain future work. Domain health checks are also still listed as a verification plan.

## Lab Environment

| Component | Configuration |
|---|---|
| Hypervisor | Oracle VirtualBox |
| Server OS | Windows Server 2022 Standard Evaluation |
| Server | `DC01` — `192.168.10.10` |
| Domain | `lab.local` |
| Management tools | Active Directory Users and Computers; Windows PowerShell |

## Security Groups and Membership

The full exercise is now [Part 3: Security Groups and Membership](security-groups/README.md), following server setup and user creation.

## Future Work

- Complete deployment documentation and verify Active Directory and DNS health.
- Verify the remaining group scopes, assign resource permissions through groups, and test access.
- Capture final CLIENT02 placement and sign-in evidence, configure DHCP, and practice Group Policy.

---

This is a personal homelab for learning and skills development, not a production enterprise deployment.

[Begin Part 1: Windows Server and AD DS Setup](server-setup/README.md) · [Back to homelab projects](../README.md)
