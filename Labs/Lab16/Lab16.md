# Lab 16: Creating an ELK Use Case for Monitoring Credential Dumping Using Mimikatz

## Step 1: Open Kibana Discover

In Kibana, open:

**Kibana → Discover**

Select the following:

**Data View:**

```text
logs-*
```

**Time Range:**

```text
Last 15 minutes
```

---

## Step 2: Generate a Suspicious PowerShell Process

On **Windows Server 2019**, open **PowerShell as Administrator**.

Run:

```powershell
powershell.exe -ExecutionPolicy Bypass
```

Then exit it by typing:

```powershell
exit
```

This simply creates a PowerShell process that Sysmon will log. It does not perform any malicious action.

---

## Step 3: Verify Process Creation Events

Open:

**Kibana → Discover**

Run the following KQL query:

```text
winlog.channel:"Microsoft-Windows-Sysmon/Operational" AND event.code:1
```

You should see the PowerShell process creation event.

---

## Step 4: Create the Detection Query

Here we will take a copy of any log and find out:

- `event.code`
- `event.provider`
- `winlog.channel`
- `winlog.event_data.Image`
- `DestinationIp`
- `DestinationPort`

Use these fields to analyze the event and identify the process responsible for the activity.

---

## Result

The PowerShell process creation event can be detected using **Sysmon Event ID 1** in Kibana.

This demonstrates how ELK and Sysmon can be used to monitor suspicious PowerShell process activity.
