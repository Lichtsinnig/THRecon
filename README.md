# THRecon

-Threat Hunting Reconnaissance Toolkit-

A collection of PowerShell modules designed for artifact gathering and reconnaisance of Windows-based endpoints. Use cases include incident response triage, threat hunting, baseline monitoring, snapshot comparisons, and more.

|       [Host Info](https://github.com/TonyPhipps/THRecon/wiki/Computer)       | [Processes](https://github.com/TonyPhipps/THRecon/wiki/Processes)* |      [Services](https://github.com/TonyPhipps/THRecon/wiki/Services)      | [Autoruns](https://github.com/TonyPhipps/THRecon/wiki/Autoruns) |      [Drivers](https://github.com/TonyPhipps/THRecon/wiki/Drivers)      |
| :--------------------------------------------------------------------------: | :----------------------------------------------------------------: | :-----------------------------------------------------------------------: | :-------------------------------------------------------------: | :---------------------------------------------------------------------: |
|                                     ARP                                      |      [DLLs](https://github.com/TonyPhipps/THRecon/wiki/DLLs)*      |                                  EnvVars                                  |                           Hosts File                            |                                   ADS                                   |
|            [DNS](https://github.com/TonyPhipps/THRecon/wiki/DNS)             |                              Strings*                              | [Users & Groups](https://github.com/TonyPhipps/THRecon/wiki/GroupMembers) |    [Ports](https://github.com/TonyPhipps/THRecon/wiki/Ports)    | [Select Registry](https://github.com/TonyPhipps/THRecon/wiki/Registry)  |
|                                   Hotfixes                                   |                              Handles*                              |                                  Sofware                                  |                            Hardware                             |   [Event Logs](https://github.com/TonyPhipps/THRecon/wiki/EventLogs)    |
|                                 Net Adapters                                 |                             Net Routes                             |                                 Sessions                                  |                             Shares                              | [Certificates](https://github.com/TonyPhipps/THRecon/wiki/Certificates) |
| [Scheduled Tasks](https://github.com/TonyPhipps/THRecon/wiki/ScheduledTasks) |                                TPM                                 |                                 Bitlocker                                 |                           Recycle Bin                           |                               User Files                                |


* Ingest using your SIEM of choice (_Check out [THRecon-Elasticstack](https://github.com/TonyPhipps/THRecon-Elasticstack) and [SIEM Tactics](https://github.com/TonyPhipps/SIEM)_)
______________________________________________________

## Index

  * [Quick Start](#quick-start)
  * [Usage](#usage)
  * [Analysis](#analysis)
  * [Troubleshooting](#troubleshooting)
  * [Screenshots](#screenshots)
  
______________________________________________________

## Quick Start

### Requirements

* Requires Powershell 5.0 or above on the "scanning" device.
* Requires Powershell 3.0 or higher on target systems. You can make this further backward compatible to PowerShell 2.0 by replacing instances of "Get-CIMinstance" with "Get-WMIObject"
* When scanning a remote machine without the psexec wrapper (Invoke-THR_PSExec), requires WinRM service on remote machine.

### Install with [Git](https://gitforwindows.org/)

In a Command or PowerShell console, type the following...

```
git clone https://github.com/TonyPhipps/THRecon C:\Users\$env:UserName\Documents\WindowsPowerShell\Modules\THRecon
```

To update...

```
cd $ENV:USERPROFILE\Documents\WindowsPowerShell\Modules\THRecon
git pull
```

### Install with PowerShell

Copy/paste this into a PowerShell console

```
$Modules = "$ENV:USERPROFILE\Documents\WindowsPowerShell\Modules\"
New-Item -ItemType Directory $Modules\THRecon\ -force
Invoke-WebRequest https://github.com/TonyPhipps/THRecon/archive/master.zip -OutFile $Modules\master.zip
Expand-Archive $Modules\master.zip -DestinationPath $Modules
Copy-Item $Modules\THRecon-master\* $Modules\THRecon\ -Force -Recurse
Remove-Item  $Modules\THRecon-master -Recurse -Force
```

Functions can also be used by opening the .psm1 file and copy-pasting its entire contents into a PowerSell console.

To update, simply run the same block of commands again.

## Run THRecon!

This command will output results of a scan against localhost to c:\temp\

```
Invoke-THR -Quick -Output c:\temp\
```

## Analysis

Analysis methodologies and techniques are provided in the [Wiki pages](https://github.com/TonyPhipps/THRecon/wiki).

## Troubleshooting
[Installing a Powershell Module](https://msdn.microsoft.com/en-us/library/dd878350(v=vs.85).aspx)

If your system does not automatically load modules in your user [profile](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_profiles?view=powershell-6), you may need to [import the module manually](https://msdn.microsoft.com/en-us/library/dd878284(v=vs.85).aspx).

```
cd $ENV:USERPROFILE\Documents\WindowsPowerShell\Modules\THRecon\
Import-Module .\THRecon.psm1
```

## Screenshots

Output of Command "Invoke-THR"

![Output of Command "invoke-thr -verbose"](https://i.imgur.com/zcmra0v.png)

Output Files

![Output Files](https://i.imgur.com/D3kpjun.png)


## Similar Projects

- https://github.com/Invoke-IR/PowerForensics
- https://github.com/PowerShellMafia/CimSweep
- https://www.crowdstrike.com/resources/community-tools/crowdresponse/
- https://github.com/gfoss/PSRecon/
- https://github.com/n3l5/irCRpull
- https://github.com/davehull/Kansa/
- https://github.com/WiredPulse/PoSh-R2
- https://github.com/google/grr
- https://github.com/diogo-fernan/ir-rescue
- https://github.com/SekoiaLab/Fastir_Collector
- https://github.com/AlmCo/Panorama
- https://github.com/certsocietegenerale/FIR
- https://github.com/securycore/Get-Baseline
- https://github.com/Infocyte/PSHunt
- https://github.com/giMini/NOAH
- https://github.com/A-mIn3/WINspect
- https://learn.duffandphelps.com/kape
- https://www.brimorlabs.com/tools/

What makes THRecon stand out:
- Lightweight. Fits on a floppy disk!
- Very little footprint/impact on targets.
- Leverages Powershell & WMI.
- Coding style encourages proper code review, learning, and "borrowing."
- No DLLs or compiled components.