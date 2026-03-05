# Fort Reign — Automation Scripts

## FortReign.Build.ps1

Full environment provisioner for the Fort Reign Garrison 
simulation environment.

### What It Builds
- Complete Active Directory OU structure
- 30+ user accounts with realistic job titles, 
  departments, and email addresses
- Role-based security groups (Read/Write and Read-Only 
  per department)
- Department SMB file shares with NTFS permissions
- Least privilege access enforcement
- Realistic seed data in each department share
- Scheduled task for automated activity simulation

### Department Shares Created

| Share | Path | Groups |
|---|---|---|
| FRG_Command | D:\FortReignShares\Command | FRG_Command_RW/RO |
| FRG_ITOps | D:\FortReignShares\ITOps | FRG_ITOps_RW/RO |
| FRG_SecOps | D:\FortReignShares\SecOps | FRG_SecOps_RW/RO |
| FRG_HR | D:\FortReignShares\HR | FRG_HR_RW/RO |
| FRG_Finance | D:\FortReignShares\Finance | FRG_Finance_RW/RO |
| FRG_Logistics | D:\FortReignShares\Logistics | FRG_Logistics_RW/RO |

### Seed Data Generated

| Department | Data |
|---|---|
| Command | Commander's Intent, Operations Briefs |
| ITOps | Ticket backlog CSV, runbooks |
| SecOps | SIEM detections CSV, IR playbooks |
| HR | Training tracker CSV, acceptable use policy |
| Finance | Budget lines CSV, invoice procedures |
| Logistics | Asset inventory CSV, shipping checklists |

### Usage
```powershell
# Run as Domain Admin on LAB-DC01
.\FortReign.Build.ps1

# Custom parameters
.\FortReign.Build.ps1 `
  -SharesRoot "D:\FortReignShares" `
  -DefaultUserPassword "P@ssw0rd!ChangeMe" `
  -BusinessStartHour 8 `
  -BusinessEndHour 17
```

### Security Notes
- Script enforces least privilege — removes Everyone 
  and Authenticated Users from share permissions
- Default password requires change at first logon
- Teardown script available for lab resets
- Idempotent — safe to re-run without duplicating objects

## FortReign.Teardown.ps1

Lab reset script. Removes all Fort Reign AD objects, 
shares, and scheduled tasks. Destructive operations 
are commented out by default — review before running.

## Activity Simulation

The build script installs a scheduled task that runs 
every 15 minutes during business hours generating:
- File read/write events on department shares
- Authentication events (Event ID 4624/4625)
- Baseline telemetry for SIEM tuning

Simulation logs stored at:
```
C:\ProgramData\FortReignSim\activity.log
```