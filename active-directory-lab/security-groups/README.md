# Part 3: Security Groups and Membership

[Previous: Part 2 — User Creation](../user-creation/README.md) · [Lab overview](../README.md) · [Next: Part 4 — Client Domain Joins](../client-domain-join/README.md)

Building on the [user-creation lab](../user-creation/README.md), I organized role groups centrally and added Alice Johnson to Helpdesk using **Active Directory Users and Computers (ADUC)**. This exercise demonstrates directory organization, group configuration, and membership administration as a foundation for group-based access.

### Directory Design and Current Results

User accounts remain under `lab.local/_Branches/Denver/Users`. The centralized `_Groups` OU sits directly under `lab.local`, alongside `_Branches`, so role groups can be managed separately from branch user accounts.

```text
lab.local
├── _Branches
│   └── Denver
│       └── Users
│           ├── Alice Johnson
│           ├── Bob Martinez
│           └── Chris Walker
└── _Groups
    ├── Helpdesk       [created; Alice Johnson is a member]
    ├── Accounting     [created; scope not yet verified]
    └── ITSupport      [created; scope not yet verified]
```

*Relevant portion of the verified directory structure. The design calls for Global Security groups; only Helpdesk has a properties screenshot confirming scope.*

| Item | Configuration or result | Status |
|---|---|---|
| Centralized group OU | `OU=_Groups,DC=lab,DC=local` | Created; visible at the domain root |
| Helpdesk | Global scope, Security type | Created and verified in group properties |
| Alice Johnson | Member of Helpdesk; account remains in Denver Users | Verified in Helpdesk's Members tab |
| Accounting and ITSupport | Security groups in `_Groups`; Global scope intended | Creation verified; scope not shown in the list view |
| Resource access | Assign permissions to a group and test member access | Future work |

### Selected Evidence

![Alice Johnson, Bob Martinez, and Chris Walker in the Denver Users OU](../user-creation/images/04-three-users-created.png)

*Denver user accounts — The existing user-creation result establishes the three accounts in `_Branches/Denver/Users` before the security-group exercise.*

![Helpdesk, Accounting, and ITSupport listed in the centralized _Groups OU](../images/security-groups/03-centralized-groups-created.png)

*All three groups created — The root-level `_Groups` OU contains Helpdesk, Accounting, and ITSupport. The Type column identifies them as security groups; this view does not establish their scope.*

![Helpdesk properties showing Global scope and Security type, with the root-level _Groups OU visible](../images/security-groups/01-helpdesk-global-security.png)

*Centralized group management — Helpdesk's General tab confirms Global scope and Security type. The directory tree also shows `_Groups` directly beneath `lab.local`.*

![Helpdesk Members tab showing Alice Johnson and her Denver Users directory location](../images/security-groups/02-helpdesk-alice-member.png)

*Membership verified — Alice Johnson appears in Helpdesk's Members tab, with her account location still shown as `lab.local/_Branches/Denver/Users`.*

### OU vs. Security Group

An **organizational unit (OU)** organizes directory objects and provides a place to delegate administration and link Group Policy. Placing Alice in the Denver Users OU does not automatically make her a member of Helpdesk or grant access to a shared folder.

A **security group** collects security principals, such as user accounts, so rights and resource permissions can be assigned to the group. Alice can remain in her branch OU while belonging to a role group stored in `_Groups`.

**Global scope** fits a role group whose members come from the same domain: it can contain accounts and other Global groups from `lab.local`. Global does not mean unrestricted access. **Security type** makes the group usable for permissions; a Distribution group is intended for email distribution and cannot be used in resource access-control lists. See [Microsoft's security-group reference](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-groups).

### Account → Group → Permission

```text
Verified:  Alice Johnson → member of Helpdesk
Future:    Helpdesk → permission on a resource → test Alice's effective access
```

The completed work establishes the **account → group** relationship. Creating Helpdesk and adding Alice does not by itself grant new resource access. The next stage is to assign a defined resource permission through a group and test the result. Managing access through groups makes role changes easier to review than maintaining separate permissions for every user.

No resource ACL changes, group nesting, or successful access tests are claimed here. Bob and Chris's Helpdesk membership is also not demonstrated.

**Skills demonstrated:** OU organization, Global Security group configuration, ADUC membership administration, and verification of account-to-group relationships.

## Next Steps

- Verify Global scope for Accounting and ITSupport in their group properties.
- Assign resource permissions through groups and test effective access.

---

[Previous: Part 2 — User Creation](../user-creation/README.md) · [Lab overview](../README.md) · [Next: Part 4 — Client Domain Joins](../client-domain-join/README.md)
