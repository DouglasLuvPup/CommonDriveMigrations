# Common Drive Migration - System Documentation

Automated file share migration system for migrating on-premises Common Drive data to Microsoft Teams/SharePoint Online using SPMT (SharePoint Migration Tool).

## Overview

This solution provides:
- **Distributed Processing**: 6 servers × 3 SPMT instances = 18 parallel workers
- **Timezone-aware Scheduling**: Migrations run during off-hours based on user's local timezone
- **Priority Queuing**: FIFO processing with priority levels 1-10
- **App-only Authentication**: Certificate-based, fully unattended operation
- **Automatic Cleanup**: Post-migration source deletion with safety checks

## Documentation

📄 **[View Full Documentation](SystemDocumentation.html)** - Open in browser for best experience

## Architecture Diagrams

### Migration Process Flow
![Migration Process Flow](diagrams/migration-process-flow.png)

### System Architecture
![System Architecture](diagrams/system-architecture.png)

## Key Features

| Feature | Description |
|---------|-------------|
| **18 Parallel Workers** | 6 servers × 3 SPMT instances for distributed processing |
| **Timezone Windows** | EST, CST, MST, PST, AKST, HST + ANYTIME option |
| **Large Migration Handling** | Items ≥10GB restricted to weekends/holidays |
| **Claim-based Locking** | Prevents duplicate processing |
| **7-Year Data Filter** | Only migrates files modified within last 7 years |
| **Empty Folder Cleanup** | Triple-verified before deletion |

## Components

| Script | Purpose |
|--------|---------|
| `CommonDriveMigration.v2.ps1` | Main migration orchestrator |
| `SPMT-Worker.v2.ps1` | SPMT execution worker |
| `Invoke-UNCStorageScan-v2.ps1` | Source folder scanner |
| `Update-MigrationTargets.v2.ps1` | Teams/storage resolution |
| `Import-MigrationSources.ps1` | Bulk CSV import utility |
| `New-MigrationDashboard.ps1` | Statistics dashboard generator |
| `New-MigrationLandingPage.ps1` | Division landing page |

## Prerequisites

- Windows Server 2016+
- PowerShell 5.1+
- SharePoint Migration Tool (SPMT) 4.2+
- PnP.PowerShell module 1.12+
- Azure AD App Registration with Sites.FullControl.All

## Quick Start

1. **Create SPO List** - `CommonMigrationStatus` with required columns
2. **Register Azure Apps** - 31 apps for distributed throttling
3. **Deploy Scripts** - Copy to all migration servers
4. **Configure Scheduled Tasks** - UNC Scan, Target Resolution, SPMT Workers
5. **Add Migration Items** - Populate list with source paths

## License

This project is provided as-is for reference and learning purposes.

## Author

Douglas Cox - Microsoft Customer Success Architect
