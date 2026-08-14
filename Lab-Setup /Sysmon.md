# Sysmon Setup in Windows Server 2019

## Step 1: Open Browser

Open your browser and go to:

```text
https://learn.microsoft.com/sysinternals/downloads/sysmon
```

Download the **Sysmon.zip** file.

---

## Step 2: Create Sysmon Directory

Open PowerShell and run:

```powershell
mkdir C:\Sysmon
```

---

## Step 3: Copy Sysmon Files

Run:

```powershell
Copy-Item "C:\Users\riddh\Downloads\Sysmon\*" "C:\Sysmon\" -Recurse
```

---

## Step 4: Verify Sysmon Files

Run:

```powershell
dir C:\Sysmon
```

You should see:

```text
Eula.txt
Sysmon.exe
Sysmon64.exe
Sysmon64a.exe
```

---

## Step 5: Download Sysmon Configuration

Run:

```powershell
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/SwiftOnSecurity/sysmon-config/master/sysmonconfig-export.xml" -OutFile "C:\Sysmon\sysmonconfig-export.xml"
```

---

## Step 6: Verify Configuration File

Run:

```powershell
dir C:\Sysmon
```

Now you should see:

```text
Eula.txt
Sysmon.exe
Sysmon64.exe
Sysmon64a.exe
sysmonconfig-export.xml
```

---

## Step 7: Navigate to Sysmon Directory

Run:

```powershell
cd C:\Sysmon
```

---

## Step 8: Install Sysmon

Run:

```powershell
.\Sysmon64.exe -accepteula -i .\sysmonconfig-export.xml
```

You should see something similar to:

```text
System Monitor v15.xx
Sysmon installed.
SysmonDrv installed.
Configuration file installed.
```

---

## Step 9: Verify Sysmon Service

Run:

```powershell
Get-Service Sysmon64
```

You should see:

```text
Status   Name       DisplayName
------   ----       -----------
Running  Sysmon64   Sysmon64
```
