# Network Printer Setup

A modern, user-friendly Windows application for installing network printers from a print server. Built with .NET 8.0 WPF and Material Design. **No admin rights required!**

# Both app are still in testing and looking for feedback
- **Macos editions:** https://github.com/hov172/MacNetworkPrinterSharedUtility 
## ✨ Key Features

- **🔓 NO ADMIN RIGHTS REQUIRED**: Standard users can install network printers!
- **📦 SINGLE FILE EXECUTABLE**: Self-contained - no .NET installation required (~164 MB)
- **🌐 Multi-Protocol Support**: SMB (Windows), IPP (Linux/CUPS), or Both
- ** Modern Material Design UI**: Professional interface with Pantone 343C green theme
- **💻 Full Command Line Support**: Complete CLI for enterprise deployment and automation
- **🤫 Silent Mode**: Unattended installation for logon scripts and mass deployment
- **⚙️ Persistent Settings**: Configuration saved and remembered between sessions
- **🔍 Smart Discovery**: WMI-based printer enumeration from Windows Print Servers
- **📦 Batch Installation**: Install multiple printers simultaneously with progress tracking
- **📊 Progress Tracking**: Real-time installation progress with detailed status
- **🔄 Async Operations**: Non-blocking UI - no freezing during network operations
- **🛡️ Error Handling**: Comprehensive error reporting and logging
- **🎯 Filter & Search**: Find printers quickly with real-time search
- **🖨️ Full Management**: Set default, print test pages, remove printers
- **⌨️ Keyboard Shortcuts**: F5 (refresh), Ctrl+R (reload), Ctrl+F (search), Ctrl+, (settings)

## 📋 Requirements

- **Operating System**: Windows 10/11 (64-bit) or Windows Server 2016+
- **Runtime**: None! Self-contained executable includes .NET 8.0 runtime
- **Permissions**: Standard user - NO administrator rights required
- **Network**: Access to Windows Print Server (SMB share or IPP protocol)

## 🚀 Quick Start

### GUI Mode (Interactive)

1. **Run the Application**
   ```cmd
   NetworkPrinterApp.exe
   ```

2. **Configure Settings** (first run only)
   - Click the **Settings** button (gear icon)
   - Enter your print server address (e.g., `printserver.domain.com`)
   - Choose protocol: **SMB** (Windows) or **IPP** (Linux/CUPS)
   - Click **Test Connection** to verify
   - Click **Save**

3. **Install Printers**
   - Printers will load automatically after settings are saved
   - Select printers from the list using checkboxes
   - Click **Install Selected**
   - Wait for installation to complete - **no admin prompt needed!**

### Silent Mode (Automated)

Install all available printers without GUI:

```cmd
NetworkPrinterApp.exe -Silent -PrintServer printserver.domain.com
```

## � MSI Installer for Enterprise Deployment

For enterprise environments, a **Windows Installer (MSI) package** is available that provides:

- ✅ **Silent Installation**: Deploy via GPO, SCCM, Intune, or scripts
- ✅ **Automatic PATH Configuration**: Adds installation directory to system PATH
- ✅ **All Users Installation**: Installs to `C:\Program Files\Ayala Solutions\Network Printer Setup\`
- ✅ **Start Menu Shortcuts**: Creates shortcuts in "Ayala Solutions" folder
- ✅ **Command-Line Arguments**: Pre-configure print server during installation
- ✅ **Proper Uninstallation**: Clean removal via Windows Programs & Features

### Quick MSI Installation

#### Interactive Installation
```cmd
msiexec /i NetworkPrinterSetup.msi
```

#### Silent Installation with Print Server Pre-Configuration
```cmd
msiexec /i NetworkPrinterSetup.msi /quiet PRINTSERVER="printserver.domain.com" PROTOCOL="SMB" SILENTINSTALL="1" AUTOINSTALL="1"
```

### Available MSI Properties

| Property | Description | Example |
|----------|-------------|---------|
| `PRINTSERVER` | Pre-configure print server address | `PRINTSERVER="printserverFQDN"` |
| `PROTOCOL` | Set protocol: SMB, IPP, or Both | `PROTOCOL="SMB"` |
| `SILENTINSTALL` | Run app in silent mode after install | `SILENTINSTALL="1"` |
| `AUTOINSTALL` | Auto-install all printers after launch | `AUTOINSTALL="1"` |
| `CREATESHORTCUT` | Create Start Menu shortcut (default: 1) | `CREATESHORTCUT="0"` |
| `CREATEDESKTOPSHORTCUT` | Create Desktop shortcut | `CREATEDESKTOPSHORTCUT="1"` |

### MSI Deployment Examples

#### Deploy via Group Policy (Silent + Auto-Install)
```cmd
msiexec /i "\\fileserver\deployment\NetworkPrinterSetup.msi" /quiet PRINTSERVER="printserver.domain.com" SILENTINSTALL="1" AUTOINSTALL="1"
```

#### Deploy via SCCM/ConfigMgr
```cmd
msiexec /i NetworkPrinterSetup.msi /qn PRINTSERVER="printserver.domain.com" PROTOCOL="SMB" AUTOINSTALL="1"
```

#### Interactive Install with Pre-Configuration
```cmd
msiexec /i NetworkPrinterSetup.msi PRINTSERVER="printserver.domain.com" PROTOCOL="IPP"
```

### PATH Environment Variable

The MSI installer automatically adds the installation directory to the system PATH, allowing you to run the application from any command prompt:

```cmd
# After MSI installation, you can run from anywhere:
NetworkPrinterApp.exe -Silent -PrintServer printserver.domain.com
```

The PATH entry is automatically removed during uninstallation.

### Building the MSI Installer

For detailed instructions on building, customizing, and troubleshooting the MSI installer, see:

📘 **[Installer Documentation](Installer/README.md)**

Topics covered:
- Building the installer from source
- Customizing installer behavior
- Advanced deployment scenarios
- Troubleshooting installation issues
- Manual PATH configuration

## �💻 Command Line Reference

### Syntax

```
NetworkPrinterApp.exe [OPTIONS]
```

### Available Options

| Option | Alias | Description | Example |
|--------|-------|-------------|---------|
| `-Silent` | `/silent` | Run without GUI and install all new printers | `-Silent` |
| `-AutoInstall` | `/autoinstall` | Launch GUI and automatically install all printers | `-AutoInstall` |
| `-ShowAll` | `/showall` | Include already installed printers in the list | `-ShowAll` |
| `-ForceReinstall` | `/forcereinstall` | Reinstall printers even if already installed | `-ForceReinstall` |
| `-PrintServer <address>` | `/printserver <address>` | Specify print server address | `-PrintServer printserver01.domain.com` |
| `-Help` | `/help`, `-?`, `/?` | Display help information | `-Help` |

### Command Line Examples

#### 1. Basic GUI Launch

```cmd
NetworkPrinterApp.exe
```

Opens the GUI with default settings.

#### 2. Silent Mode - Install All New Printers

```cmd
NetworkPrinterApp.exe -Silent -PrintServer printserver.domain.com
```

- Runs without GUI
- Connects to specified print server
- Installs all printers not currently installed
- Shows console output with progress
- Returns exit code

#### 3. GUI with Auto-Install

```cmd
NetworkPrinterApp.exe -AutoInstall -PrintServer printserver01
```

- Opens GUI
- Automatically starts installation of all listed printers
- User can see progress in real-time

#### 4. Show All Printers (Including Installed)

```cmd
NetworkPrinterApp.exe -ShowAll
```

- Opens GUI
- Displays both installed and uninstalled printers
- Useful for troubleshooting or reinstalling

#### 5. Force Reinstall in Silent Mode

```cmd
NetworkPrinterApp.exe -Silent -ForceReinstall -PrintServer printserver.domain.com
```

- Runs without GUI
- Reinstalls all printers, even if already installed
- Useful for driver updates or fixing broken installations

#### 6. Override Server from Settings

```cmd
NetworkPrinterApp.exe -PrintServer backup-printserver.domain.com
```

- Opens GUI
- Uses specified server instead of saved settings
- Settings file is NOT updated

#### 7. Combination: Silent + Force + Custom Server

```cmd
NetworkPrinterApp.exe -Silent -ForceReinstall -PrintServer emergency-server.domain.local
```

- Silent mode (no GUI)
- Reinstalls all printers
- Uses emergency backup server

#### 8. Display Help

```cmd
NetworkPrinterApp.exe -Help
```

Shows built-in help with all available options.

### Exit Codes

The application returns standardized exit codes for automation and scripting:



| Code | Constant | Description |:: Run GUI and show all printers, including installed ones

|------|----------|-------------|NetworkPrinterApp.exe -ShowAll

| `0` | `SUCCESS` | All operations completed successfully |

| `0` | `SUCCESS` | All operations completed successfully |
| `1` | `PARTIAL_SUCCESS` | Some printers installed, but some failed |
| `2` | `ALL_PRINTERS_FAILED` | All printer installations failed |
| `3` | `NO_PRINTERS_FOUND` | No printers discovered on server |
| `4` | `UNEXPECTED_ERROR` | Unhandled exception occurred |
| `10` | `NO_SERVER_CONFIGURED` | No print server address provided |
| `11` | `INVALID_SERVER` | Default/placeholder server address detected |
| `12` | `SERVER_UNREACHABLE` | Unable to connect to print server |

### Batch Script with Error Handling

```batch
@echo off
echo Installing network printers...

NetworkPrinterApp.exe -Silent -PrintServer printserver.domain.com

if %ERRORLEVEL% EQU 0 (
    echo SUCCESS: All printers installed
    exit /b 0
)

if %ERRORLEVEL% EQU 1 (
    echo WARNING: Some printers failed to install
    exit /b 1
)



if %ERRORLEVEL% EQU 3 (
    echo INFO: No new printers to install
    exit /b 0
)

if %ERRORLEVEL% EQU 12 (
    echo ERROR: Cannot reach print server
    exit /b 12
)

echo ERROR: Installation failed with code %ERRORLEVEL%
exit /b %ERRORLEVEL%
```

### PowerShell Script with Error Handling

```powershell
# Install network printers with error handling
$printServer = "printserver.domain.com"

Write-Host "Installing network printers from $printServer..." -ForegroundColor Cyan

$process = Start-Process -FilePath "NetworkPrinterApp.exe" `
    -ArgumentList "-Silent", "-PrintServer", $printServer `
    -Wait -PassThru -NoNewWindow

switch ($process.ExitCode) {
    0 {
        Write-Host "✓ SUCCESS: All printers installed successfully" -ForegroundColor Green
        exit 0
    }

    1 {```powershell

        Write-Warning "⚠ PARTIAL: Some printers installed, some failed"# Regular PowerShell parameter handling

        exit 1param (

    }    [switch]$Silent = $false,

    1 {
        Write-Host "⚠ WARNING: Some printers failed to install" -ForegroundColor Yellow
        exit 1
    }
    3 {
        Write-Host "ℹ INFO: No new printers to install" -ForegroundColor Yellow
        exit 0
    }
    10 {
        Write-Error "✗ ERROR: No print server configured"
        exit 10
    }
    12 {
        Write-Error "✗ ERROR: Cannot reach print server: $printServer"
        exit 12
    }
    default {
        Write-Error "✗ ERROR: Installation failed with code $($process.ExitCode)"
        exit $process.ExitCode
    }
}
```

## 🚀 Enterprise Deployment

### Group Policy Logon Script

#### Method 1: User Logon Script (Silent Installation)

1. **Create logon script** (`install-printers.cmd`):

```batch
@echo off
\\fileserver\deployment\NetworkPrinterApp.exe -Silent -PrintServer printserver.domain.com
```



2. **Deploy via Group Policy**:### 📊 Enhanced GUI with Server Information Display

   - Open **Group Policy Management**```powershell

   - Edit policy → **User Configuration** → **Policies** → **Windows Settings** → **Scripts (Logon/Logoff)**# Add server info label (for debugging)

   - Add script: `\\fileserver\deployment\install-printers.cmd`$serverLabel = New-Object System.Windows.Forms.Label

$serverLabel.Location = New-Object System.Drawing.Point(10, 450)

#### Method 2: Scheduled Task (Run at Logon)$serverLabel.Size = New-Object System.Drawing.Size(580, 20)

$serverLabel.Text = "Print Server: $printServerAddress"

1. **Create Scheduled Task via GPO**:$form.Controls.Add($serverLabel)

   - **Computer Configuration** → **Preferences** → **Control Panel Settings** → **Scheduled Tasks**```

   - **Action**: Create

   - **Trigger**: At log on (any user or specific user)The GUI now includes a visible label showing which print server is being used, making it easier to verify the connection settings, especially when using the `-PrintServer` parameter to override the default.

   - **Action**: Start a program

     - **Program**: `\\fileserver\deployment\NetworkPrinterApp.exe`### 🗒️ Improved Logging with Approved PowerShell Verbs

     - **Arguments**: `-Silent -PrintServer printserver.domain.com````powershell

   - **Settings**:function Write-Log {

     - ☑ Run whether user is logged on or not    param ([string]$message)

     - ☐ Run with highest privileges (NOT needed!)    Add-Content -Path $logFile -Value "$(Get-Date -Format 'u') - $message"

     - ☑ Start the task only if the computer is on AC power (optional)    Write-Output $message

}

### SCCM/ConfigMgr Deployment```

The script uses the `Write-Log` function (following PowerShell's approved verb standards) to log all actions to both a temporary log file (`%TEMP%\PrinterInstallLog.txt`) and the console output, making it easier to troubleshoot issues.

**Package Properties:**

- **Program Name**: Install Network Printers### 🖨️ Proper Null Comparison for Installed Printers

- **Command Line**: `NetworkPrinterApp.exe -Silent -PrintServer printserver.domain.com````powershell

- **Run**: Hidden$installedConnections = Get-Printer |

- **Program can run**: Whether or not a user is logged on    Where-Object { $null -ne $_.ComputerName } |

- **Run mode**: Run with user's rights (NOT administrative rights)    ForEach-Object { "\\$($_.ComputerName)\$($_.ShareName)".Trim() }

```

### Microsoft Intune DeploymentThe script builds an array of already installed network printers using proper PowerShell null comparison syntax with `$null` on the left side of comparisons for consistent behavior with collections and arrays.



**Win32 App Configuration:**### 🌐 Enhanced Printer List Function with Approved Verbs

- **Install command**: ```powershell

  ```cmdfunction Update-PrinterList {

  NetworkPrinterApp.exe -Silent -PrintServer printserver.domain.com    $allPrinters = Get-Printer -ComputerName $printServerAddress |

  ```        Where-Object { $_.Shared -eq $true -and $_.ShareName } |

- **Uninstall command**: N/A (printers can be removed via Windows Settings)        Sort-Object -Property ShareName -Unique

- **Install behavior**: User
- **Return codes**: Configure success=0, soft reboot=1, hard reboot=0, fail=2-12
- **Detection rule**: Custom script to check if printers are installed

### Microsoft Intune Deployment

1. **Package as Win32 app** (.intunewin)
2. **Install command**: `NetworkPrinterApp.exe -Silent -PrintServer printserver.domain.com`
3. **Uninstall command**: Not applicable (printers remain installed)
4. **Detection rule**: Custom PowerShell script to check installed printers
5. **Requirements**: Windows 10/11 64-bit
6. **Assignment**: Deploy to users or devices

### Network Share Deployment

1. **Copy executable to network share**:

   ```cmd
   copy NetworkPrinterApp.exe \\fileserver\deployment\
   ```

2. **Create wrapper script for logging**:

   ```batch
   @echo off
   set LOGFILE=\\fileserver\logs\%COMPUTERNAME%_printer_install.log
   echo %DATE% %TIME% - Starting printer installation >> %LOGFILE%
   \\fileserver\deployment\NetworkPrinterApp.exe -Silent -PrintServer printserver.domain.com >> %LOGFILE% 2>&1
   echo %DATE% %TIME% - Exit code: %ERRORLEVEL% >> %LOGFILE%
   ```

### Pre-Deploy Configuration File

You can pre-deploy the settings file to users' AppData folders for zero-configuration deployment:

**Location**: `%APPDATA%\NetworkPrinterApp\settings.json`



**Example settings.json**:## 📝 Important Notes for Customization

```json

{To adapt this app to your environment:

  "PrintServer": "printserver.domain.com",

  "Protocol": "SMB",1. **Update the Default Print Server**:

  "ShowAll": false,   - Edit line 24 in the script:

  "ForceReinstall": false,   ```powershell

  "RememberSettings": true,   [string]$PrintServer = "PrintServerFQDN"

  "LastUsedServer": "printserver.domain.com",   ```

  "CheckForUpdatesOnStartup": false,   - Replace "PrintServerFQDN" with your actual print server address (e.g., "print-server.domain.com")

  "ConnectionTimeoutSeconds": 30,

  "FilterByUserAccess": false2. **Custom Deployment Considerations**:

}   - When compiling with 
```   - Test the executable with and without parameters to ensure correct behavior

   - The log file at `%TEMP%\PrinterInstallLog.txt` can help troubleshoot parameter issues

**Deploy via GPO**:

```batch3. **Parameter Handling**:

@echo off   - The script now uses a consistent approach to parameter handling

if not exist "%APPDATA%\NetworkPrinterApp" mkdir "%APPDATA%\NetworkPrinterApp"   - The default PrintServer value is maintained across both script and executable modes

copy /Y "\\fileserver\config\settings.json" "%APPDATA%\NetworkPrinterApp\settings.json"   - The GUI displays the active PrintServer value for verification

```

---

## 🎯 Use Cases

## 📄 License

### 1. IT Help Desk

```cmdMIT License *(or institutional license if required)*

NetworkPrinterApp.exe -ShowAll

```---

- See all printers (installed and available)

- Troubleshoot printer issues## 👨‍💼 Maintain and Build

- Reinstall problematic printers

**Sarah Lawrence College – ITS Help Desk Department - Jesus Ayala**

### 2. New Employee Onboarding

```cmd> For bugs or enhancements, please open an issue.

NetworkPrinterApp.exe -AutoInstall -PrintServer printserver.domain.com
```
- Automatically install all department printers
- User watches progress in GUI
- No technical knowledge required

### 3. Bulk Deployment (Logon Script)
```cmd
NetworkPrinterApp.exe -Silent -PrintServer printserver.domain.com
```
- Runs at user logon
- No user interaction
- Installs all new printers automatically

### 4. Disaster Recovery (Force Reinstall)
```cmd
NetworkPrinterApp.exe -Silent -ForceReinstall -PrintServer printserver.domain.com
```
- Reinstall all printers from scratch
- Useful after driver updates
- Fixes broken printer connections

### 5. Multi-Site Deployment
```batch
@echo off
:: Determine site based on computer name or AD site
if "%COMPUTERNAME:~0,3%"=="NYC" (
    NetworkPrinterApp.exe -Silent -PrintServer printserver-nyc.domain.com
) else if "%COMPUTERNAME:~0,3%"=="LAX" (
    NetworkPrinterApp.exe -Silent -PrintServer printserver-lax.domain.com
) else (
    NetworkPrinterApp.exe -Silent -PrintServer printserver-main.domain.com
)
```

### 6. Department-Specific Deployment
```powershell
# Get user's department from Active Directory
$user = [System.Security.Principal.WindowsIdentity]::GetCurrent().Name
$searcher = [adsisearcher]"(samaccountname=$($user.Split('\')[1]))"
$department = $searcher.FindOne().Properties.department

# Install printers based on department
switch ($department) {
    "Finance" { 
        Start-Process "NetworkPrinterApp.exe" "-Silent -PrintServer finance-print.domain.com" -Wait 
    }
    "HR" { 
        Start-Process "NetworkPrinterApp.exe" "-Silent -PrintServer hr-print.domain.com" -Wait 
    }
    "IT" { 
        Start-Process "NetworkPrinterApp.exe" "-Silent -PrintServer it-print.domain.com" -Wait 
    }
    default { 
        Start-Process "NetworkPrinterApp.exe" "-Silent -PrintServer printserver.domain.com" -Wait 
    }
}
```

## 🔐 Security & Permissions

### Why NO Admin Rights Required?

The application uses the Windows `AddPrinterConnection` API which:
- ✅ Designed for standard users
- ✅ Connects to network printers without elevation
- ✅ Drivers are provided by the print server (Point and Print)
- ✅ Only installs user-level printer connections

### What Can Standard Users Do?

✅ **Allowed**:
- Install network printers from configured print servers
- Remove printers they installed
- Set default printer
- Print test pages
- View printer properties

❌ **NOT Allowed** (requires admin):
- Install local printers
- Install printer drivers manually
- Modify print server settings
- Add new print servers to GPO

### Security Best Practices

1. **Use Group Policy Print Server List**:
   - Configure allowed print servers via GPO
   - Prevents users from connecting to unauthorized servers

2. **Enable Point and Print Restrictions**:
   - Configure via GPO: `Computer Configuration\Policies\Administrative Templates\Printers`
   - Restrict driver installation to trusted servers only

3. **Audit Printer Installation**:
   - Enable audit logging for printer events
   - Monitor which users install which printers

4. **Deploy via Trusted Location**:
   - Place executable on secured network share
   - Use NTFS permissions to control access

5. **Code Signing** (recommended):
   - Sign the executable with your organization's certificate
   - Prevents tampering and builds trust

## 🎨 User Interface Features

### Main Window

- **Printer List**: Sortable DataGrid with printer name, location, and status
- **Search Box**: Real-time filtering (Ctrl+F to focus)
- **Connection Status**: Live indicator showing server connection state
- **Batch Selection**: Select multiple printers with checkboxes
- **Progress Bar**: Real-time installation progress
- **Status Messages**: Clear feedback on all operations
- **Material Design**: Professional green theme (Pantone 343C)

### Keyboard Shortcuts

- **F5** or **Ctrl+R**: Refresh printer list
- **Ctrl+F**: Focus search box
- **Ctrl+,**: Open settings
- **Ctrl+A**: Select all printers (in list)
- **Space**: Toggle selection on focused printer

### Settings Window

- **Print Server**: Server address configuration
- **Protocol Selection**: Radio buttons for SMB vs IPP
- **Connection Test**: Validate server before saving
- **Advanced Options**: Timeout, filtering, auto-update
- **Remember Settings**: Persistent configuration

## 🌐 IPP (Internet Printing Protocol) Support

### Overview

In addition to the traditional SMB/CIFS protocol for Windows print servers, the application now supports **IPP (Internet Printing Protocol)**. This enables connection to:

- **Linux/UNIX Print Servers**: CUPS (Common UNIX Printing System)
- **macOS Print Servers**: Built-in macOS print sharing
- **Cross-Platform Environments**: Mixed Windows/Linux networks
- **Cloud Print Services**: IPP-compatible cloud printing solutions
- **Modern Printers**: Many network printers have built-in IPP support
- **AirPrint Printers**: AirPrint-enabled printers (see AirPrint section below)

### IPP vs AirPrint: What's the Difference?

**Short Answer**: AirPrint is Apple's implementation of IPP with additional features.

| Aspect | IPP | AirPrint |
|--------|-----|----------|
| **Protocol Base** | Standard IPP (RFC 2910, 2911) | IPP + Apple extensions |
| **Standard Body** | IETF/PWG (Internet standards) | Apple proprietary |
| **Compatibility** | Cross-platform (Windows, Linux, macOS, etc.) | Apple devices (iOS, iPadOS, macOS) |
| **Authentication** | Standard IPP auth | Apple-specific auth |
| **Discovery** | DNS-SD (Bonjour), manual | Bonjour/mDNS (automatic) |
| **Print Features** | Basic IPP capabilities | Enhanced (duplex, color, finishing) |
| **Driver Requirement** | May require driver on client | Driverless (built-in iOS/macOS) |
| **PDF Support** | Standard PDF | Apple PDF extensions |

**Key Points**:

✅ **AirPrint printers ARE IPP printers** - They support standard IPP protocol
✅ **This app CAN connect to AirPrint printers** - Using the IPP protocol option
✅ **You don't get Apple-specific features** - Windows doesn't support AirPrint extensions
✅ **Works with most AirPrint printers** - Basic printing functionality available

### Can I Use This App with AirPrint Printers?

**YES!** Most AirPrint-enabled printers support standard IPP and can be used with this application:

#### Steps to Connect to AirPrint Printer:

1. **Find the printer's IP address**:
   - Check printer's display panel/menu
   - Print network configuration page
   - Check your router's DHCP client list

2. **Configure in Network Printer Setup**:
   - Open Settings (Ctrl+,)
   - Select **IPP** protocol
   - Enter printer address: `192.168.1.100` or `printer.local`
   - Test connection

3. **Install the printer**:
   - Printer should appear in the list
   - Select and click "Install Selected"

#### Example AirPrint Printer Brands:

- **HP**: Most OfficeJet, LaserJet, and Envy printers
- **Canon**: PIXMA, imageCLASS, and MAXIFY series
- **Epson**: WorkForce, EcoTank, and Expression series
- **Brother**: Most modern network printers
- **Xerox**: Modern network MFPs
- **Ricoh**: Network-enabled printers

### 🔍 Automatic Printer Discovery (NEW!)

**Network Printer Setup now includes automatic IPP/AirPrint printer discovery!**

The application features **dual discovery modes** to find printers both on your local subnet and across different network segments:

#### Discovery Features

✅ **mDNS/Bonjour Discovery** - Automatically finds AirPrint/IPP printers on your local subnet
✅ **Multi-Subnet Scanning** - Scan additional networks where printers are located
✅ **Configurable Timeout** - Adjust scan timeout for large networks (default: 30 seconds)
✅ **Seamless Integration** - Discovered printers appear alongside server printers
✅ **Cross-VLAN Support** - Find printers on different subnets/VLANs

#### How to Use Discovery

1. **Open Settings** (Ctrl+, or click Settings button)

2. **Select IPP Protocol** (or "Both")

3. **Enable mDNS Discovery** (enabled by default)
   - Discovers printers on your local subnet using Bonjour/mDNS
   - Finds printers advertising `_ipp._tcp.local` and `_ipps._tcp.local` services

4. **Add Additional Subnets** (optional - for cross-VLAN/cross-subnet discovery)
   - Click **"Add Subnet"** in the IPP Discovery section
   - Enter subnet prefix (e.g., `192.168.1`, `10.0.5`, `172.16.10`)
   - Add multiple subnets for different networks
   - Application will scan all 254 addresses in each subnet

5. **Adjust Scan Timeout** (optional)
   - Default: 30 seconds
   - Increase for larger networks or slower connections
   - Decrease for faster scanning

6. **Save Settings** and **Refresh Printer List**
   - Discovery runs automatically when loading printers
   - Status shows: "Discovering IPP/AirPrint printers..."
   - Then: "Scanning 2 additional subnet(s)..." (if configured)

#### Discovery Examples

**Example 1: Same Subnet Discovery**
```
Protocol: IPP
mDNS Discovery: ✅ Enabled
Additional Subnets: (none)

Result: Finds all AirPrint/IPP printers on local subnet (e.g., 192.168.1.x)
```

**Example 2: Multi-Subnet Enterprise Network**
```
Protocol: IPP
mDNS Discovery: ✅ Enabled
Additional Subnets:
  - 10.0.5      (Marketing VLAN)
  - 10.0.10     (Engineering VLAN)
  - 192.168.50  (Guest Network)

Result: 
  - Finds printers on your subnet via mDNS
  - Scans 10.0.5.1-254 for IPP printers (port 631)
  - Scans 10.0.10.1-254 for IPP printers
  - Scans 192.168.50.1-254 for IPP printers
```

**Example 3: Remote Office**
```
Protocol: IPP
mDNS Discovery: ✅ Enabled
Additional Subnets:
  - 172.16.20   (Remote office subnet)

Result: Discovers printers in both local and remote office
```

#### What Gets Discovered?

The discovery service finds:

- **AirPrint-enabled printers** (HP, Canon, Epson, Brother, etc.)
- **Linux CUPS print servers** sharing via IPP
- **macOS print servers** with printer sharing enabled
- **Network printers with IPP support** (most modern printers)
- **Print servers on other subnets** (via subnet scanning)

**Information Retrieved**:
- Printer name
- IP address
- Hostname (if DNS reverse lookup succeeds)
- Port (usually 631)
- Service type (_ipp._tcp or _ipps._tcp)

#### Technical Details

**mDNS Discovery**:
- Protocol: Bonjour/mDNS (multicast DNS)
- Service Types: `_ipp._tcp.local` and `_ipps._tcp.local`
- Timeout: 10 seconds
- Scope: Local subnet only (multicast limitation)
- Library: Tmds.MDns

**Subnet Scanning**:
- Method: TCP connect to port 631
- Range: All 254 addresses per subnet (x.x.x.1-254)
- Timeout: Configurable (default 30 seconds)
- Parallel: Scans multiple addresses simultaneously
- Firewall-friendly: Uses standard TCP connections

#### Network Requirements

**For mDNS Discovery**:
- ✅ Same subnet/VLAN as printer
- ✅ UDP port 5353 not blocked by firewall
- ✅ Multicast traffic allowed
- ⚠️ Does NOT work across subnets/VLANs

**For Subnet Scanning**:
- ✅ Network routing between subnets (if different VLAN)
- ✅ TCP port 631 accessible to printer
- ✅ Firewall allows outbound connections
- ✅ Works across subnets/VLANs

#### Troubleshooting Discovery

**No printers found via mDNS?**
1. Verify printer is AirPrint/IPP compatible
2. Check printer is on same subnet
3. Verify firewall allows UDP 5353 (multicast)
4. Try subnet scanning instead (add your subnet to Additional Subnets)

**Subnet scanning not finding printers?**
1. Verify subnet prefix is correct (e.g., `192.168.1` not `192.168.1.0`)
2. Check network routing allows connection to that subnet
3. Verify firewall allows TCP port 631 to printers
4. Increase scan timeout for slower networks
5. Check printer has IPP enabled (port 631 open)

**Discovery is slow?**
1. Reduce number of additional subnets
2. Decrease scan timeout (if printers respond quickly)
3. Disable mDNS if not needed
4. Only scan subnets where printers are located

### AirPrint Printer Discovery (Legacy Documentation)

**IPP/AirPrint printers ARE discoverable within a subnet** using Bonjour/mDNS (multicast DNS). The application now includes:

- ✅ **CAN** connect to AirPrint printers via direct IP or hostname
- ✅ **CAN** auto-discover AirPrint printers via Bonjour/mDNS (NEW!)
- ✅ **CAN** scan additional subnets for IPP printers (NEW!)
- ℹ️ See "Automatic Printer Discovery" section above for configuration

#### How AirPrint/IPP Discovery Works

**Technical Details**:

1. **Protocol**: Bonjour/mDNS (multicast DNS) on UDP port 5353
2. **Service Types**: 
   - `_ipp._tcp.local` - Standard IPP printers
   - `_ipps._tcp.local` - Secure IPP (IPP over TLS)
   - `_printer._tcp.local` - Legacy printer service
3. **Scope**: Subnet-only (multicast doesn't route between subnets)
4. **Platform Support**:
   - ✅ macOS/iOS - Built-in Bonjour support
   - ✅ Linux - Avahi daemon (Bonjour compatible)
   - ⚠️ Windows - Bonjour service must be installed (via iTunes, Bonjour Print Services, or standalone)

#### Why This App Doesn't Auto-Discover (Yet)

**Current Limitation**: This application requires manual IP address entry because:

1. **mDNS Library Required**: Would need to add Bonjour/mDNS client library (e.g., `Tmds.MDns`)
2. **Windows Compatibility**: Windows doesn't have native mDNS support (needs Apple's Bonjour service)
3. **Network Security**: Some enterprise networks block multicast traffic (UDP 5353)
4. **Subnet Limitation**: Multicast discovery only works within the same subnet/VLAN
5. **Implementation Complexity**: Current focus is on SMB server discovery and manual IPP entry

**Future Enhancement**: Auto-discovery of AirPrint/Bonjour printers may be added in future versions.

#### How to Find IPP/AirPrint Printers on Your Network

Even though the app doesn't auto-discover, you can find IPP/AirPrint printers using these methods:

##### Method 1: Printer's Display Panel
Most modern printers show their IP address:
- Press **Menu** or **Settings** button
- Navigate to **Network** or **Network Settings**
- Look for **IP Address** or **TCP/IP**
- Example: `192.168.1.50`

##### Method 2: Print Network Configuration Page
Most printers can print their network info:
- Press **Menu** → **Reports** → **Network Configuration**
- Or press and hold **Print** button for 5+ seconds
- Look for IP address on printed page

##### Method 3: Router's DHCP Client List
Check your router's admin page:
1. Open router admin (usually `192.168.1.1` or `192.168.0.1`)
2. Find **DHCP Clients**, **Connected Devices**, or **Network Map**
3. Look for printer name/model
4. Note the assigned IP address

##### Method 4: Bonjour Browser (Recommended)
**Download a Bonjour browser tool** to see all discoverable printers:

**Free Tools**:
- [Bonjour Browser](https://hobbyistsoftware.com/bonjourbrowser) (Windows/macOS)
- [Discovery - DNS-SD Browser](https://apps.apple.com/app/discovery-dns-sd-browser/id1381004916) (macOS)
- [Service Browser](https://play.google.com/store/apps/details?id=com.druk.servicebrowser) (Android)

**How to use**:
1. Install and run Bonjour Browser
2. Look for services: `_ipp._tcp` or `_ipps._tcp`
3. Click on a printer to see:
   - Hostname (e.g., `HP-LaserJet-Pro.local`)
   - IP Address (e.g., `192.168.1.50`)
   - Port (usually 631)
4. Use this information in Network Printer Setup

##### Method 5: Windows Command Line (if Bonjour installed)
If you have Apple's Bonjour service installed (comes with iTunes):

```cmd
:: List Bonjour services
dns-sd -B _ipp._tcp local
```

Or use PowerShell (Windows 10 1809+):
```powershell
# Resolve mDNS services (requires Windows 10 1809+)
Resolve-DnsName -Name "_ipp._tcp.local" -Type PTR
```

##### Method 6: Network Scanner Tools
Use network scanning tools to find printers:

```powershell
# PowerShell: Scan subnet for IPP printers
1..254 | ForEach-Object {
    $ip = "192.168.1.$_"
    if (Test-NetConnection -ComputerName $ip -Port 631 -InformationLevel Quiet) {
        Write-Host "IPP printer found at: $ip" -ForegroundColor Green
    }
}
```

Or use **nmap** (cross-platform tool):
```bash
# Scan subnet for IPP printers
nmap -p 631 --open 192.168.1.0/24
```

##### Method 7: Check DNS for .local Addresses
If you know the printer's hostname:
```powershell
# Try resolving .local address
ping HP-LaserJet-Pro.local
```

#### Subnet Limitations for IPP/AirPrint Discovery

**Important Network Considerations**:

| Network Scenario | Auto-Discovery | Manual Connection | Notes |
|------------------|----------------|-------------------|-------|
| **Same Subnet** | ✅ Possible (with tools) | ✅ Yes | Multicast works within subnet |
| **Different Subnet/VLAN** | ❌ No | ✅ Yes (if routed) | Multicast doesn't cross subnets |
| **Across VPN** | ❌ No | ⚠️ Maybe | Depends on VPN configuration |
| **Corporate Network with mDNS Gateway** | ✅ Possible | ✅ Yes | Some enterprise networks use mDNS gateways |
| **Isolated WiFi (Guest)** | ❌ No | ❌ No | AP isolation blocks all discovery |

**Key Point**: Even if you can't auto-discover the printer, you can usually still connect if you know its IP address or hostname, as long as network routing and firewall rules allow it.

#### Making IPP/AirPrint Printers Easier to Find

**Network Administrator Tips**:

1. **Use DHCP Reservations**: Assign static IP addresses via DHCP
   - Printer always gets same IP (e.g., `192.168.1.50`)
   - Users can bookmark the IP address

2. **Create DNS Records**: Add A records for printers
   - `printer1.company.local` → `192.168.1.50`
   - Easier to remember than IP addresses

3. **Document Printer IPs**: Maintain a list of printer IPs
   - Share with IT team and users
   - Include in onboarding documentation

4. **Deploy mDNS Gateway**: For multi-subnet networks
   - Allows Bonjour discovery across VLANs
   - Examples: Avahi with reflector, multicast router

5. **Enable Bonjour on Windows**: Pre-install Bonjour service
   - Comes with iTunes
   - Or deploy standalone Bonjour Print Services
   - Enables `.local` hostname resolution

6. **Use Print Server**: Centralize IPP printers
   - Set up CUPS server as a relay
   - Windows users connect to CUPS server
   - CUPS server handles printer discovery

### AirPrint vs Windows Printing

When using an AirPrint printer from Windows via IPP:

| Feature | AirPrint (iOS/macOS) | This App (Windows via IPP) |
|---------|----------------------|----------------------------|
| Basic Printing | ✅ Yes | ✅ Yes |
| Color Printing | ✅ Yes | ✅ Yes (if driver supports) |
| Duplex (2-sided) | ✅ Yes | ⚠️ Depends on Windows driver |
| Paper Size Selection | ✅ Yes | ✅ Yes |
| Print Quality | ✅ Yes | ✅ Yes |
| Finishing Options | ✅ Yes | ⚠️ Limited (driver dependent) |
| Auto-Discovery | ✅ Yes (Bonjour) | ❌ No (manual IP/hostname) |
| Driverless Printing | ✅ Yes | ⚠️ May need driver |

### Troubleshooting AirPrint Printers on Windows

#### Problem: Can't find AirPrint printer

**Solutions**:
1. Find printer IP address from printer menu
2. Try `.local` address: `PrinterName.local`
3. Use Bonjour Browser (free tool) to discover printers
4. Check if printer and PC are on same network/VLAN
5. Disable AP isolation on wireless router

#### Problem: Connection fails to AirPrint printer

**Solutions**:
1. Verify printer supports standard IPP (most do)
2. Try port 631 explicitly: `192.168.1.100:631`
3. Check if printer requires authentication
4. Disable any "AirPrint only" mode on printer
5. Update printer firmware

#### Problem: Printer installs but won't print

**Solutions**:
1. Install generic IPP printer driver on Windows
2. Try "Microsoft IPP Class Driver"
3. Check if manufacturer provides Windows IPP driver
4. Verify paper size compatibility
5. Check print queue for errors

### Using Bonjour Browser to Find AirPrint Printers

**Bonjour Browser** (free tool) can help you find AirPrint printers on your network:

1. **Download**: [Bonjour Browser](https://hobbyistsoftware.com/bonjourbrowser) or similar mDNS browser
2. **Run**: Launch Bonjour Browser
3. **Look for**: Services named `_ipp._tcp` or `_ipps._tcp`
4. **Get Details**: Click on printer to see IP address and port
5. **Use in App**: Enter the IP address in Network Printer Setup

**Alternative**: Use PowerShell to discover mDNS services:
```powershell
# Requires Windows 10 1809+ with mDNS support
Resolve-DnsName -Name "_ipp._tcp.local" -Type PTR
```

### Converting AirPrint URL to Windows Format

AirPrint printers advertise URLs like:
```
ipp://Brother-HL-L2350DW._ipp._tcp.local:631/ipp/print
```

**For this application, use**:
```
Brother-HL-L2350DW.local
```
or the IP address:
```
192.168.1.50
```

The application automatically adds the IPP protocol and port.

### When to Use IPP vs SMB

| Scenario | Recommended Protocol | Why |
|----------|---------------------|-----|
| Windows Print Server | **SMB** | Native Windows protocol, full feature support |
| Linux CUPS Server | **IPP** | Standard Linux printing protocol |
| macOS Print Server | **IPP** | macOS native print sharing uses IPP |
| Mixed Environment | **Both** | Let users choose based on their server |
| Firewall Restrictions | **IPP** | Port 631 may be more permissive than 445 |
| Internet/Remote Printing | **IPP** | Designed for network printing |
| Legacy Windows | **SMB** | Older Windows servers only support SMB |

### IPP Configuration

#### GUI Configuration

1. Open **Settings** (Ctrl+,)
2. Enter your print server address:
   - Format: `printserver.domain.com` or IP address
   - Port is optional (defaults to 631)
3. Select **IPP** protocol radio button
4. Click **Test Connection** to verify
5. Click **Save**

#### Command-Line Configuration

IPP is configured via the settings file. Once set in GUI, it's used for all operations:

```cmd
:: First, configure IPP via GUI, then use silent mode
NetworkPrinterApp.exe -Silent -PrintServer cups-server.domain.com
```

The protocol selection is saved in settings.json and automatically used.

### IPP Server Addresses

#### CUPS Server (Linux)
```
http://cups-server.domain.com:631
```
or simply:
```
cups-server.domain.com
```
(port 631 is assumed)

#### macOS Print Server
```
macos-server.local
```
or:
```
macos-server.domain.com
```

#### Direct IPP Printer
```
printer.domain.com
```
or:
```
192.168.1.100
```

### IPP Discovery Process

When IPP protocol is selected, the application:

1. **Connects** to the specified server on port 631
2. **Queries** available printers using IPP Get-Printers operation
3. **Lists** all IPP-shared printers
4. **Displays** printer names, locations, and status
5. **Installs** selected printers using Windows IPP printer port

### IPP Advantages

✅ **Cross-Platform**:
- Works with Windows, Linux, macOS servers
- Industry-standard protocol (RFC 2910, RFC 2911)

✅ **Firewall-Friendly**:
- Uses HTTP/HTTPS (port 631 or 443)
- Can traverse firewalls more easily than SMB

✅ **Secure**:
- Supports IPP-over-HTTPS (IPPS)
- TLS/SSL encryption available
- Authentication supported

✅ **Feature-Rich**:
- Printer capabilities discovery
- Job status monitoring
- Printer status queries

### IPP Limitations

⚠️ **Considerations**:
- **Driver Installation**: May require manual driver installation for some printers
- **Windows Print Server**: Not the native protocol for Windows
- **Feature Support**: Some Windows-specific features may not work
- **Performance**: Slightly higher overhead than SMB on local networks

### Troubleshooting IPP

#### Problem: "Unable to connect to IPP server"

**Solutions**:
1. Verify server address and port:
   ```cmd
   Test-NetConnection -ComputerName cups-server.domain.com -Port 631
   ```
2. Check firewall allows port 631
3. Verify CUPS or IPP service is running on server
4. Try with IP address instead of hostname
5. Check if HTTPS/port 443 is required

#### Problem: "No printers found on IPP server"

**Solutions**:
1. Verify printers are shared on CUPS/IPP server
2. Check printer permissions (may require authentication)
3. Verify IPP server configuration allows printer discovery
4. Check CUPS web interface: `http://server:631`
5. Test with `ipptool` command on Linux:
   ```bash
   ipptool -tv ipp://server:631/printers/ get-printers.test
   ```

#### Problem: "Printer installs but won't print"

**Solutions**:
1. Verify correct printer driver is installed on Windows
2. Check print queue on IPP server
3. Test print directly to IPP URL:
   ```cmd
   notepad /pt testpage.txt \\server\printer
   ```
4. Verify user has print permissions on IPP server
5. Check CUPS logs on Linux server: `/var/log/cups/error_log`

### CUPS Server Setup (Linux)

For IT administrators setting up a CUPS server for Windows clients:

```bash
# Install CUPS
sudo apt-get install cups

# Enable remote administration
sudo cupsctl --remote-admin --remote-any --share-printers

# Add Windows client access
sudo nano /etc/cups/cupsd.conf
```

**cupsd.conf configuration**:
```
# Allow access from Windows clients
<Location />
  Order allow,deny
  Allow @LOCAL
</Location>

<Location /printers>
  Order allow,deny
  Allow @LOCAL
</Location>
```

**Restart CUPS**:
```bash
sudo systemctl restart cups
```

**Share a printer**:
```bash
lpoptions -p PrinterName -o printer-is-shared=true
```

### macOS Server Setup

To enable IPP printing from macOS:

1. **System Settings** → **Printers & Scanners**
2. Select printer → **Share this printer on the network**
3. Firewall: Allow IPP (port 631)

Windows clients can then connect using:
```
macos-server.local
```

### IPP URL Formats

The application supports various IPP URL formats:

| Format | Example | Usage |
|--------|---------|-------|
| Hostname | `cups-server.domain.com` | Standard CUPS server |
| Hostname:Port | `printserver.domain.com:631` | Custom port |
| IP Address | `192.168.1.50` | Direct IP connection |
| IP:Port | `192.168.1.50:631` | IP with custom port |
| Full IPP URL | `ipp://server.domain.com:631/printers/` | Explicit IPP URL |
| IPPS (Secure) | `ipps://server.domain.com:443/printers/` | Encrypted IPP |

### Security Considerations for IPP

1. **Use IPPS when possible** (IPP over TLS/SSL)
2. **Configure authentication** on CUPS server
3. **Restrict IP ranges** in cupsd.conf
4. **Use VPN** for remote IPP access
5. **Enable logging** to monitor access

### Example: Mixed Environment Deployment

For organizations with both Windows and Linux print servers:

**config.json for Site A (Windows)**:
```json
{
  "PrintServer": "printserver-win.domain.com",
  "Protocol": "SMB"
}
```

**config.json for Site B (Linux)**:
```json
{
  "PrintServer": "cups-server.domain.com",
  "Protocol": "IPP"
}
```

**Deployment script**:
```batch
@echo off
:: Detect server type and deploy appropriate config
if exist \\printserver-win\print$ (
    copy config-smb.json %APPDATA%\NetworkPrinterApp\settings.json
) else (
    copy config-ipp.json %APPDATA%\NetworkPrinterApp\settings.json
)
NetworkPrinterApp.exe -Silent
```

### IPP Performance Tips

1. **Use hostname resolution**: Ensure DNS is working properly
2. **Close firewall gaps**: Allow port 631 bidirectionally
3. **Limit printer list**: Large CUPS servers may have discovery delays
4. **Use local CUPS relay**: Set up local CUPS server as a relay for remote IPP servers
5. **Monitor network latency**: IPP is more sensitive to latency than SMB

## 🐛 Troubleshooting

### Problem: "Unable to connect to print server"

**Solutions**:
1. Verify server address: ping `printserver.domain.com`
2. Check firewall: SMB port 445, IPP port 631
3. Verify DNS resolution
4. Try IP address instead of hostname
5. Check user permissions on print server

### Problem: "No printers found"

**Solutions**:
1. Verify printers are shared on server
2. Check user permissions to view shared printers
3. Try `-ShowAll` parameter to see installed printers
4. Verify print server has printers configured
5. Check that printers are published to AD

### Problem: Printers install but don't print

**Solutions**:
1. Check printer is online
2. Verify print queue status
3. Test print from server directly
4. Check driver compatibility
5. Reinstall with `-ForceReinstall`

### Problem: Application crashes or freezes

**Solutions**:
1. Check error log: Look for `error_log.txt` in app directory
2. Run with `-Help` to verify command-line parsing
3. Check antivirus exclusions
4. Try running from command prompt to see console errors
5. Verify single-file executable is complete (164 MB)

### Problem: "Access Denied" errors

**Solutions**:
1. Verify user is NOT running as admin (can cause issues)
2. Check print server Point and Print settings
3. Verify Group Policy print restrictions
4. Ensure user has "Print" permission on shared printers
5. Check that print server allows standard user connections

## 📊 Logging

### Silent Mode Console Output

When running in silent mode, detailed logging is written to console:

```
Network Printer Setup - Silent Mode
Print Server: printserver.domain.com
Force Reinstall: False

Testing connection to print server...
Connection successful.
Discovering available printers...
Found 5 printer(s) to install:
  - HR-Printer (Building A, Room 101)
  - Finance-Printer (Building B, Room 205)
  - IT-Printer (Building C, Room 301)
  - Reception-Printer (Building A, Lobby)
  - Legal-Printer (Building B, Room 410)

Installing printers...
Installing 1/5: HR-Printer
Installing 2/5: Finance-Printer
Installing 3/5: IT-Printer
Installing 4/5: Reception-Printer
Installing 5/5: Legal-Printer

Installation Summary:
  Installed: 5
  Skipped: 0
  Failed: 0

Exit Code: 0 - All operations completed successfully

Press any key to exit...
```

### GUI Logging

- Real-time status messages in main window
- Progress bar with current operation
- Detailed results dialog after installation
- Error messages with actionable guidance

## 📦 Building from Source

### Configuration Options

```json
{
  "PrintServer": "printserver.domain.com",
  "Protocol": "SMB",
  "ShowAll": false,
  "ForceReinstall": false,
  "RememberSettings": true,
  "LastUsedServer": "printserver.domain.com",
  "CheckForUpdatesOnStartup": false,
  "ConnectionTimeoutSeconds": 30,
  "FilterByUserAccess": false
}
```

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `PrintServer` | string | empty | Print server FQDN or IP address |
| `Protocol` | enum | SMB | Protocol to use (SMB or IPP) |
| `ShowAll` | boolean | false | Show installed printers in list |
| `ForceReinstall` | boolean | false | Reinstall existing printers |
| `RememberSettings` | boolean | true | Save settings between sessions |
| `LastUsedServer` | string | empty | Last successfully used server |
| `CheckForUpdatesOnStartup` | boolean | false | Check for app updates on launch |
| `ConnectionTimeoutSeconds` | integer | 30 | Server connection timeout |
| `FilterByUserAccess` | boolean | false | Only show printers user can access |

## 📝 Version History

### Version 2.0.0 (Current - October 2025)
- ✨ Renamed to "Network Printer Setup"
- ✨ Self-contained single-file executable (no .NET runtime required)
- ✨ Multi-protocol support (SMB + IPP)
- ✨ Async/await pattern (no UI freezing)
- ✨ Keyboard shortcuts (F5, Ctrl+R, Ctrl+F, Ctrl+,)
- ✨ Real-time search and filtering
- ✨ First-run configuration wizard
- ✨ Enhanced Material Design UI
- ✨ Comprehensive command-line interface
- ✨ Standardized exit codes for automation
- 🐛 Fixed radio button selection visibility
- 🐛 Fixed Settings window crash on first run
- 🐛 Fixed application not continuing after settings save
- 📦 Icon appears in all windows (main + settings + taskbar)

### Version 1.0.0 (Initial Release)
- Initial release as "Network Printer Setup"
- Basic SMB support
- GUI printer installation
- Settings persistence

## 📄 License

MIT License

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

### Development Guidelines

1. Follow C# coding conventions
2. Use async/await for I/O operations
3. Add XML documentation comments
4. Update README for new features
5. Test on Windows 10 and 11
6. Ensure single-file publish works correctly

## 📧 Support

For issues, questions, or feature requests:
- Open an issue on GitHub
- Contact your IT department
- Review the troubleshooting section above

## 👤 Credits

**Framework**: .NET 8.0 WPF with MaterialDesignInXamlToolkit
**License**: MIT
**Icon Design**: Custom Pantone 343C green printer icon

---

**🎉 Thank you for using Network Printer Setup!**

*Making printer installation easy for everyone - no admin rights required.*


