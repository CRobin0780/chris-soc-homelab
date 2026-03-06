# Windows Server Active Directory — LAB-DC01

## Server Details
- VM ID: 401
- Hostname: LAB-DC01
- Node: pve-t7810
- OS: Windows Server 2022
- RAM: 10GB | Disk: 60GB

## Domain Configuration
- Domain Name: lab.local
- NetBIOS Name: LAB
- Domain Functional Level: Windows Server 2016
- Forest Functional Level: Windows Server 2016

## Roles Installed
- Active Directory Domain Services (AD DS)
- DNS Server
- File and Storage Services

## Organizational Unit Structure
```
lab.local/
├── FortReign/
│   ├── Command
│   ├── Computers
│   ├── Finance
│   ├── Groups
│   ├── HR
│   ├── IT_Operations
│   ├── Logistics
│   ├── Security_Operations
│   ├── Service_Accounts
│   └── Users
├── HQ-Clients
├── HQ-Servers
├── HQ-Users
└── Managed Service Accounts
```

## Security Configuration
- Account Lockout Policy: Pending GPO hardening
- Password Policy: Pending GPO hardening
- Audit Policy: Pending configuration
- CIS Benchmark: Pending implementation

## NIST 800-53 Control Mapping
- AC-2: Account Management — OU structure supports
- IA-5: Authenticator Management — Password policy pending
- AU-2: Event Logging — Audit policy pending
- CM-6: Configuration Settings — CIS GPO pending

## Time Synchronization

| VM | Time Source | Stratum | Status |
|---|---|---|---|
| LAB-DC01 | time.windows.com | 4 | ✅ Synced |
| FRG-FS01 | LAB-DC01 (192.168.20.21) | 5 | ✅ Synced |
| FRG-MGMT01 | LAB-DC01 (192.168.20.21) | 5 | ✅ Synced |

NTP hierarchy: time.windows.com → LAB-DC01 → domain members