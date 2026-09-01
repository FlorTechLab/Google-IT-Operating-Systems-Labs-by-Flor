# Windows User and Permission Management Lab

Practical Windows administration lab focused on **local user management, local groups, NTFS permissions, Access Control Lists (ACLs), and permission inheritance using PowerShell**.

This lab was developed as part of the **Operating Systems and You: Becoming a Power User** course.

> 📄 This repository includes complete lab documentation in both Spanish and English.

---

## Lab Overview

The goal of this lab was to simulate a basic Windows administration environment where users are organized into groups and access to different resources is controlled through NTFS permissions.

The lab follows this administration model:

```text
Users
│
├── Ana ────────→ LabUsers
├── Carlos ─────→ ProjectTeam
└── AdminLab ───→ LabAdmins
```

These groups were then assigned different levels of access to resources inside `C:\CompanyLab`.

---

## Environment

- Windows 11 Pro
- PowerShell
- NTFS file system
- Windows virtual machine
- macOS host

---

## Lab Scenario

Three local users were created:

| User | Group | Role |
|---|---|---|
| `Ana` | `LabUsers` | Standard lab user |
| `Carlos` | `ProjectTeam` | Project team user |
| `AdminLab` | `LabAdmins` | Lab administrative user |

The `LabAdmins` group was created specifically for this lab and should not be confused with the built-in Windows `BUILTIN\Administrators` group.

---

## Resource Structure

The following directory structure was created to simulate organizational resources:

```text
C:\CompanyLab
│
├── Public
├── Documents
└── Projects
    ├── ProjectA
    └── ProjectB
```

This structure was later used to configure and test NTFS permissions and inheritance.

---

## NTFS Permission Model

Permissions were assigned to **groups instead of individual users**.

| Group | Resource | Permission |
|---|---|---|
| `LabUsers` | `C:\CompanyLab\Public` | Read & Execute (`RX`) |
| `ProjectTeam` | `C:\CompanyLab\Projects` | Modify (`M`) |
| `LabAdmins` | `C:\CompanyLab` | Full Control (`F`) |

This demonstrates a group-based access model where users obtain access to resources through their group memberships.

---

## Local User Management

Local users were created with PowerShell using `New-LocalUser`.

```powershell
$password = Read-Host "Enter password for Ana" -AsSecureString
New-LocalUser -Name "Ana" -Password $password

Get-LocalUser -Name "Ana"
```

`Read-Host -AsSecureString` was used to prevent passwords from being entered as visible plain text.

---

## Local Group Management

Local groups were created to organize users according to their roles.

```powershell
New-LocalGroup -Name "LabUsers" -Description "Standard users for the lab"

New-LocalGroup -Name "ProjectTeam" -Description "Users responsible for project resources"

New-LocalGroup -Name "LabAdmins" -Description "IT administrators for the lab"
```

Groups were verified using:

```powershell
Get-LocalGroup
```

---

## Group Membership

Users were assigned to their corresponding groups:

```powershell
Add-LocalGroupMember -Group "LabUsers" -Member "Ana"

Add-LocalGroupMember -Group "ProjectTeam" -Member "Carlos"

Add-LocalGroupMember -Group "LabAdmins" -Member "AdminLab"
```

Membership was verified using:

```powershell
Get-LocalGroupMember -Group "LabUsers"
Get-LocalGroupMember -Group "ProjectTeam"
Get-LocalGroupMember -Group "LabAdmins"
```

---

## ACL Inspection

Before modifying permissions, the existing Access Control List of `CompanyLab` was inspected.

```powershell
Get-Acl "C:\CompanyLab"
```

Individual access entries were inspected using:

```powershell
(Get-Acl "C:\CompanyLab").Access
```

This made it possible to identify Windows identities such as:

- `BUILTIN\Administrators`
- `NT AUTHORITY\SYSTEM`
- `BUILTIN\Users`
- `NT AUTHORITY\Authenticated Users`

The ACL inspection also introduced properties such as:

```text
FileSystemRights
AccessControlType
IdentityReference
IsInherited
InheritanceFlags
PropagationFlags
```

---

## Configuring NTFS Permissions

### LabUsers — Read & Execute

```powershell
icacls "C:\CompanyLab\Public" /grant "LabUsers:(OI)(CI)RX"
```

### ProjectTeam — Modify

```powershell
icacls "C:\CompanyLab\Projects" /grant "ProjectTeam:(OI)(CI)M"
```

### LabAdmins — Full Control

```powershell
icacls "C:\CompanyLab" /grant "LabAdmins:(OI)(CI)F"
```

Permission codes used:

| Code | Meaning |
|---|---|
| `RX` | Read & Execute |
| `M` | Modify |
| `F` | Full Control |
| `OI` | Object Inherit |
| `CI` | Container Inherit |
| `I` | Inherited |

---

## Permission Inheritance

Permission inheritance was tested using the `Projects` directory.

`ProjectTeam` received `Modify` permission on:

```text
C:\CompanyLab\Projects
```

with:

```text
(OI)(CI)M
```

The permissions of `ProjectA` were then inspected:

```powershell
icacls "C:\CompanyLab\Projects\ProjectA"
```

The `(I)` indicator confirmed that the permission was inherited from the parent directory.

```text
ProjectTeam
     │
     │ Modify
     ▼
Projects
     │
     │ inheritance
     ▼
ProjectA
     └── Modify (Inherited)
```

Because `Carlos` belongs to `ProjectTeam`, the resulting access relationship is:

```text
Carlos
  │
  ▼
ProjectTeam
  │
  ▼
Modify
  │
  ▼
Projects
  │
  ▼
ProjectA
```

---

## Verification

The final permissions were verified using:

```powershell
icacls "C:\CompanyLab\Public"
icacls "C:\CompanyLab\Projects"
icacls "C:\CompanyLab"
```

Final configuration:

```text
LabUsers    → Public     → Read & Execute (RX)
ProjectTeam → Projects   → Modify (M)
LabAdmins   → CompanyLab → Full Control (F)
```

---

## Key Concepts Practiced

- Windows local user management
- Local group management
- Group membership
- Group-based access control
- NTFS permissions
- Access Control Lists (ACLs)
- Discretionary Access Control Lists (DACLs)
- `Read & Execute`
- `Modify`
- `Full Control`
- Permission inheritance
- `ObjectInherit`
- `ContainerInherit`
- Inherited permissions
- PowerShell administration
- Permission verification with `icacls`

---

## Screenshots

The `screenshots` directory contains evidence of the main configuration and verification steps performed during the lab.

```text
screenshots/
├── 01-ana-user-created.png
├── 02-labusers-group-created.png
├── 03-projectteam-group-created.png
├── 04-labadmins-group-created.png
├── 05-ana-labusers-membership.png
├── 06-carlos-projectteam-membership.png
├── 07-adminlab-labadmins-membership.png
├── 08-groups-membership-verification.png
├── 09-companylab-structure.png
├── 10-companylab-default-acl.png
├── 11-public-labusers-permission.png
├── 12-projectteam-modify-permission.png
├── 13-labadmins-full-control.png
├── 14-project-permission-inheritance.png
└── 15-final-permissions-verification.png
```

---

## Documentation

Complete step-by-step documentation is available in both languages:

- 🇬🇧 **English:** `Windows-User-Permission-Management-Lab-EN.pdf`
- 🇪🇸 **Español:** `Windows-User-Permission-Management-Lab-ES.pdf`

---

## What I Learned

This lab helped reinforce how Windows separates **users, groups, and permissions** when controlling access to resources.

Instead of assigning permissions directly to individual users, access was managed through groups. This provided a clearer and more scalable way to control access to different directories.

The lab also demonstrated how NTFS permission inheritance works and how tools such as `Get-Acl` and `icacls` can be used to inspect, configure, and verify access control from the command line.

These concepts are directly applicable to **IT Support and Windows system administration environments**, where managing user access and troubleshooting permissions are common administrative tasks.

---

## Author

**Florencia Horita**
