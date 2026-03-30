# Veeam AsBuilt Unified

![PowerShell](https://img.shields.io/badge/PowerShell-5.1%20%7C%207-blue.svg)
![Veeam](https://img.shields.io/badge/Veeam-VBR%20%7C%20VBM365-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

---

## Overview

This script provides a unified launcher for AsBuiltReport generation for:

- Veeam Backup & Replication (VBR)
- Veeam Backup for Microsoft 365 (VBM365 / VB365)

It validates the PowerShell runtime, installs or imports the required AsBuilt modules, loads the correct Veeam PowerShell module, checks the detected product version, and generates the report in Word and HTML format.

---

## How It Works

1. Selects the target Veeam product (`VBR` or `VBM365`)  
2. Validates the PowerShell runtime required by the chosen workflow  
3. Prepares PowerShell Gallery and required dependencies  
4. Ensures the required AsBuiltReport modules are installed and imported  
5. Loads the correct Veeam PowerShell DLL  
6. Connects to the target Veeam server or service  
7. Validates the detected product version  
8. Generates the AsBuilt report in Word and HTML format  

---

## Requirements

- Veeam Backup & Replication v12+ for the VBR workflow
- Veeam Backup for Microsoft 365 v6+ for the VBM365 workflow
- PowerShell 7+ for the VBR workflow
- Windows PowerShell 5.1 for the VBM365 workflow
- Administrative rights for the VBM365 workflow
- Internet access to install required PowerShell modules from PSGallery
- AsBuiltReport compatible modules

---

## Installation

```bash
git clone https://github.com/julianscunha/Veeam.ASBuilt.Unified.git
cd Veeam.ASBuilt.Unified
```

---

## Usage

```powershell
pwsh.exe -File .\veeam_asbuilt_unified.ps1
```

---

## With parameters

```powershell
pwsh.exe -File .\veeam_asbuilt_unified.ps1 `
    -Product VBR `
    -Target localhost `
    -OutputPath "C:\Temp\AsBuiltReport_VBR"
```

```powershell
powershell.exe -File .\veeam_asbuilt_unified.ps1 `
    -Product VBM365 `
    -Target localhost `
    -OutputPath "C:\Temp\AsBuiltReport_VBM365"
```

---

## Accept TLS Certificate (for remote execution)

The current repository version does not expose a TLS bypass parameter.

If your VBR environment requires it, a future enhancement could add support for:

```powershell
Connect-VBRServer -Server "veeam01.domain.local" -ForceAcceptTlsCertificate
```

---

## Parameters

| Parameter | Description | Default |
|----------|------------|--------|
| Product | Target product: `VBR` or `VBM365` | Interactive selection |
| Target | Target server / service name | `localhost` |
| OutputPath | Output folder path | Temporary folder |
| Silent | Disables interactive confirmations where possible | Disabled |
| Relaunched | Internal flag used when switching PowerShell runtime | `0` |

---

## Log Output Example

```text
2026-03-30 22:01:10 [INFO] ===== START =====
2026-03-30 22:01:11 [INFO] Selected product: VBR
2026-03-30 22:01:12 [OK] Module loaded: AsBuiltReport.Core
2026-03-30 22:01:20 [OK] Connected successfully.
2026-03-30 22:01:25 [OK] VBR report generated successfully.
2026-03-30 22:01:30 [INFO] ===== END =====
```

---

## Important Notes

- The current repository version already contains formal comment-based help and stronger internal structure than the tape repositories  
- The script explicitly requires PowerShell 7 for the VBR workflow and Windows PowerShell 5.1 for the VBM365 workflow  
- The current code warns when VBR 13+ is detected because upstream AsBuilt module validation may lag behind product releases  
- The current repository already includes author and repository information in the script header, so the main standardization work here is visual consistency with the other repositories  

---

## Recommended Use Case

- Internal documentation generation
- Pre-upgrade and post-upgrade reporting
- Customer handoff documentation
- Environment baseline capture

---

## Scheduling Example (Windows Task Scheduler)

Program:
```text
pwsh.exe
```

Arguments:
```text
-File "C:\Scripts\veeam_asbuilt_unified.ps1" -Product VBR -Target localhost -OutputPath "C:\Temp\AsBuiltReport_VBR" -Silent
```

For VBM365, use `powershell.exe` instead of `pwsh.exe`.

---

## Future Improvements

- Add explicit TLS certificate handling for remote VBR connections
- Add parameterized report formats
- Add optional JSON / CSV execution summary
- Add better module/version matrix output
- Add support for non-interactive credential handling

---

## License

MIT License

---

## References

https://github.com/AsBuiltReport/AsBuiltReport.Veeam.VBR  
https://github.com/AsBuiltReport/AsBuiltReport.Veeam.VB365  
https://helpcenter.veeam.com/docs/vbr/powershell/  
https://helpcenter.veeam.com/docs/vbo365/powershell/  
