# SiteEdge Platform — User Manual

**Version:** 2.4  
**Audience:** Plant operators and facility managers  
**Last updated:** March 2026

---

## Introduction

SiteEdge is an industrial IoT platform that enables real-time monitoring, 
alerting, and reporting for plant equipment and facilities. This manual 
covers the core workflows for day-to-day platform use.

---

## Logging in

1. Open a supported browser and navigate to your SiteEdge portal URL.
2. Enter your email address and password.
3. Click **Sign In**.
4. If your organization uses SSO, click **Sign in with SSO** and follow your 
   identity provider's login steps.

> **Note:** After five failed login attempts, your account is locked for 
> 15 minutes. Contact your administrator to unlock it manually.

---

## Viewing the dashboard

The Dashboard provides a real-time overview of all monitored devices and 
active alerts in your organization.

**To view the dashboard:**

1. Click **Dashboard** in the left navigation panel.
2. Use the **Site** dropdown to filter by location.
3. Click a device card to view its detailed status.

**Dashboard elements**

| Element | Description |
|---|---|
| Device cards | Show status, location, and last seen time for each device |
| Alert banner | Displays the count of active high-severity alerts |
| Status indicator | Green = online, Yellow = warning, Red = offline |

---

## Managing alerts

### Viewing alerts

1. Click **Alerts** in the left navigation panel.
2. Use the **Severity** filter to narrow results.
3. Click an alert row to view full details and device history.

### Acknowledging an alert

1. Open the alert you want to acknowledge.
2. Click **Acknowledge**.
3. Enter a note describing the action taken.
4. Click **Confirm**.

> **Note:** Acknowledging an alert does not resolve it. 
> The alert remains active until the underlying condition is cleared.

### Resolving an alert

1. Open the acknowledged alert.
2. Click **Resolve**.
3. Enter a resolution note.
4. Click **Confirm**.

The alert moves to the **Resolved** tab and is removed from the active view.

---

## Generating reports

1. Click **Reports** in the left navigation panel.
2. Click **New Report**.
3. Select a report type — **Device Summary**, **Alert History**, or **Uptime Report**.
4. Set the date range using the calendar picker.
5. Click **Generate**.
6. Once generated, click **Download** to export the report as a PDF or CSV.

---

## User roles

| Role | Permissions |
|---|---|
| Viewer | View dashboard, devices, and reports |
| Operator | View and acknowledge alerts |
| Administrator | Full access including user management and API tokens |

---

## Troubleshooting

**Device shows as offline but is physically running**  
Check the network connection between the device and the SiteEdge gateway. 
Verify that the gateway service is running on the local network.

**Cannot log in**  
Ensure you are using the correct portal URL for your organization. 
If SSO is enabled, confirm with your IT team that your account is provisioned.

**Report shows no data**  
Confirm that the selected date range contains recorded data. 
Devices must be online during the reporting period to appear in reports.