# Lab 18: Creating Dashboards in ELK

## Step 1: Open Dashboards

In Kibana, navigate to:

**☰ Menu → Analytics → Dashboard**

Alternatively, search for **Dashboard** in the search bar.

---

## Step 2: Create a New Dashboard

Click:

**Create dashboard**

Then click:

**Create visualization**

---

## Step 3: Select the Data View

Choose:

```text
logs-*
```

---

## Step 4: Create Visualization-1
Choose:

**Bar Chart**

Configure:

**Y-axis:**

```text
Count
```

**X-axis:**

```text
Terms
```

**Field:**

```text
event.code
```

**Size:**

```text
10
```

Click **Save**.

Name it:

```text
Event Code Distribution
```

---

## Step 5: Add Visualization-2

Click:

**Create visualization**

Choose:

**Pie Chart**

Configure:

**Metric:**

```text
Count
```

**Slice by:**

```text
winlog.channel
```

Save as:

```text
Windows Event Channels
```

---

## Step 6: Add Visualization-3

Click:

**Create another visualization**

Choose:

**Data Table**

Add the following columns:

```text
@timestamp
event.code
host.hostname
winlog.provider_name
```

Save as:

```text
Recent Sysmon Events
```

---

## Step 7: Add Visualization-4

Create another visualization.

Choose:

**Vertical Bar Chart**

Configure:

**Y-axis:**

```text
Count
```

**X-axis:**

```text
Terms
```

**Field:**

```text
host.hostname
```

Save as:

```text
Events by Host
```

---

## Step 8: Save Dashboard

Click:

**Save**

Enter the dashboard name:

```text
SOC Monitoring Dashboard
```

---

## Result

The **SOC Monitoring Dashboard** contains multiple visualizations for monitoring security events collected through the ELK Stack.

The dashboard includes:

- Event Code Distribution
- Windows Event Channels
- Recent Sysmon Events
- Events by Host
