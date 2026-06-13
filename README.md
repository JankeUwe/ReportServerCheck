# ReportServerCheck

**SQL Server Reporting Services (SSRS/PBIRS) Diagnostic Report Suite**

A comprehensive suite of RDL-based diagnostic and monitoring reports for SQL Server Reporting Services and Power BI Report Server.

## Overview

This project contains 15+ production-ready reports that provide deep insights into SSRS/PBIRS health, performance, and configuration:

### Report Categories

- **Server Configuration & Health**: Overall instance status, feature detection
- **Report Execution & Performance**: Execution history, execution trends, performance metrics
- **Data Sources & Datasets**: Data source validation, shared dataset usage tracking
- **User Access & Permissions**: User access patterns, role assignments, subscription tracking
- **Caching & Snapshots**: Cache management, snapshot configuration and status
- **Server Inventory**: Complete catalog of all reports, folders, and subscriptions

## Features

- ✅ **SQL Server 2016+** compatible (SSRS 2016, 2017, 2019, 2022)
- ✅ **Power BI Report Server (PBIRS)** support
- ✅ **Dark Theme UI**: Professional design with Midnight Pro aesthetic
- ✅ **Zero Configuration**: Drop-in deployment via REST API
- ✅ **Shared Data Source**: `ds_ReportServer` for centralized configuration

## Deployment

### Method 1: SSRS Deployment Tool v4.0 (Recommended)

Use the companion **[SSRSDeploymentTool](https://github.com/JankeUwe/SSRSDeploymentTool)** for one-click deployment:

```
1. Open SSRS Deployment Tool
2. Select this folder as source
3. Connect to target SSRS instance
4. Click "Deploy"
```

### Method 2: Visual Studio Report Server Project

1. Open `ReportServerCheck.sln` in Visual Studio
2. Right-click project → **Deploy**
3. Configure target server in project properties

### Method 3: SSRS REST API

All reports can be deployed via SQL Server Reporting Services REST API v2.0:

```powershell
# Upload report
$headers = @{"Authorization"="Bearer $token"}
$reportBody = @{
    Name = "ReportName"
    Path = "/ReportServerCheck/ReportName"
    Content = [Convert]::ToBase64String([IO.File]::ReadAllBytes("Report.rdl"))
}
Invoke-RestMethod -Uri "$ssrsUrl/api/v2.0/Reports" `
    -Method POST -Body ($reportBody | ConvertTo-Json) -Headers $headers
```

## Data Source Configuration

All reports use a shared data source `ds_ReportServer` that must point to the **ReportServer database** on your SSRS instance:

```
Server: [Your SSRS Instance]
Database: ReportServer
Authentication: Integrated (uses SSRS service account)
```

## Requirements

- **SQL Server**: 2016 or later
- **SSRS**: 2016 or later (or Power BI Report Server)
- **Database Access**: ReportServer database (read-only sufficient)
- **Reporting Services Permissions**: Content Manager role for deployment

## Project Structure

```
ReportServerCheck/
├── ReportServerCheck.sln          # Visual Studio solution
├── ReportServerCheck.rptproj      # SSRS Report Server Project
├── ds_ReportServer.rds            # Shared data source (ReportServer DB)
├── *.rdl                          # Individual report files
└── *.rdl.data                     # Report metadata (auto-generated)
```

## License

MIT License - See LICENSE file

## Author

**Uwe Janke** | Senior IT Specialist | SQL Server & Business Intelligence

- GitHub: [@JankeUwe](https://github.com/JankeUwe)
- Website: https://www.powershelldba.de

## Support

For issues, questions, or feature requests: [Open an Issue](https://github.com/JankeUwe/ReportServerCheck/issues)

---

**Version**: 1.0  
**Last Updated**: 2026-06-13  
**Compatible with**: SSRS 2016+ / PBIRS
