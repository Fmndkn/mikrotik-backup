# MikroTik Backup Script

![RouterOS](https://img.shields.io/badge/RouterOS-7.0%2B-blue)
![MikroTik](https://img.shields.io/badge/MikroTik-Script-orange)
![FTP](https://img.shields.io/badge/Backup-FTP-green)
![Automated](https://img.shields.io/badge/Scheduled-Backup-purple)

**MikroTik script designed for scheduled configuration backup and automatic upload to FTP server**

## 📋 Description

This RouterOS script automates the process of creating encrypted configuration backups and exporting settings from your MikroTik device, then securely transfers them to a remote FTP server on a scheduled basis.

## ✨ Key Features

- **🕐 Scheduled Backups**: Configure automatic execution at set intervals
- **🔒 Encrypted Storage**: Password-protected backup files
- **☁️ Remote Storage**: Automatic FTP upload for off-device storage
- **📁 Dual Format**: Creates both `.backup` and `.rsc` export files
- **🧹 Auto Cleanup**: Removes local files after successful upload
- **📊 Detailed Logging**: Comprehensive progress tracking and error reporting

## ✨ Features

- **Automatic Naming**: Uses device name and date (e.g., `MikroTik_25-December-2024`)
- **Encrypted Backups**: Password-protected backup files
- **Dual Backup**: Both backup and export formats
- **FTP Upload**: Secure transfer to remote storage
- **Auto Cleanup**: Removes local files after upload
- **Comprehensive Logging**: Detailed progress tracking


## 🚀 Quick Start

1. **Configure FTP settings** in the script variables
2. **Upload script** to your MikroTik device
3. **Set up scheduler** for automatic execution
4. **Monitor backups** through system logs

## 🛠️ Setup

### 1. Configure Script Variables

Edit these variables in the script before deployment:

```ros
:local ftpuser "your_ftp_username"           # FTP username
:local ftppass "your_ftp_password"           # FTP password  
:local ftpaddr "your.ftp.server.com"         # FTP server address
:local ftppath "/remote/backup/path"         # Remote directory
```

### 2. Change Backup Password (Optional)
Modify the backup encryption password:

```ros
/system backup save name=$backupName password=<your_secure_password>
```

## 📥 Installation

#### Method 1: Terminal/SSH

![Setup Terminal](https://img.shields.io/badge/Setup-Terminal-lightgrey)

+ Connect to your MikroTik via SSH or WinBox terminal
+ Copy and paste the entire script content
+ Save as a system script

#### Method 2: WebFig/WinBox

![Setup WebFig](https://img.shields.io/badge/Setup-WebFig%20%7C%20FWinBox-yellow)

1. Navigate to `System` → `Scripts`

2. Click `Add New (+)`

3. Paste script content

4. Set `Name` and click `OK`

## 🚀 Usage

#### Manual Execution

![Run Manually](https://img.shields.io/badge/Run-Manually-green)

##### Terminal:

```ros
/system script run backup-script
```

##### WebFig/WinBox:

1. Go to `System` → `Scripts`

2. Find your backup script

3. Click `Run Script`

#### Automated Scheduling

![Run Automated](https://img.shields.io/badge/Run-Automated-purple)

1. Navigate to System → Scheduler

2. Add new scheduler entry:

```text
Name: daily-backup
Interval: 1d 00:00:00
On Event: /system script run backup-script
```

## 📊 Logging & Monitoring
The script provides detailed logging:

```ros
:log info "Start Backup $baseName"
:log warning "Failed to upload backup file to FTP" 
:log info "Backup completed successfully: $baseName"
```

View logs in Log section or via terminal:

```ros
/log print where message~"Backup"
```

## ⚙️ Requirements

![Requirements](https://img.shields.io/badge/Requirements-RouterOS%207.0%2B-red)


+ **RouterOS**: Version 7.0 or higher

+ **Storage**: Sufficient free space for temporary files

+ **Network**: FTP server access and internet connectivity

+ **Permissions**: Read/write access to file system

## 📝 File Structure
Generated files follow this naming pattern:

```text
[DeviceName]_[DD-Month-YYYY].backup
[DeviceName]_[DD-Month-YYYY].rsc

Example:
MikroTik_RB4011_25-December-2024.backup
MikroTik_RB4011_25-December-2024.rsc
```

## 🔒 Security Notes
+ Change the default backup password `<your_password>`

+ Consider using FTPS for secure transfers

+ Regularly rotate FTP credentials

+ Monitor backup success via logs

## 🐛 Troubleshooting
##### Backup fails to upload:

+ Verify FTP credentials and server accessibility

+ Check internet connectivity

+ Ensure FTP path exists on server

##### Script errors:

+ Confirm RouterOS version compatibility

+ Check available storage space

+ Verify script syntax in `System` → `Scripts`

## 📄 License
This script is provided as-is for MikroTik community use.
***
Need help? Check [MikroTik Documentation](https://mikrotik.com/support/) or [Community Forum](https://forum.mikrotik.com/)