# SiteEdge Release Notes

---

## Version 2.4 — March 2026

### New features

- **Bulk alert acknowledgement** — Operators can now acknowledge multiple alerts 
  simultaneously from the Alerts list view.
- **Custom report scheduling** — Reports can be scheduled to generate and email 
  automatically on a daily, weekly, or monthly basis.
- **Device grouping** — Devices can now be organised into custom groups for 
  easier filtering and reporting.

### Bug fixes

- Fixed an issue where the dashboard status indicator showed incorrect colours 
  after a browser refresh.
- Resolved a timeout error that occurred when generating Uptime Reports 
  for date ranges exceeding 90 days.
- Fixed a display issue where alert timestamps appeared in UTC instead of 
  the user's configured timezone.

### Known issues

- Bulk acknowledgement does not currently support alerts filtered by device group. 
  This will be addressed in v2.5.
- Scheduled reports may be delayed by up to 10 minutes during peak processing hours.

---

## Version 2.3 — January 2026

### New features

- **Alert escalation rules** — Administrators can configure automatic escalation 
  when an alert remains unacknowledged beyond a defined threshold.
- **API rate limit headers** — API responses now include `X-RateLimit-Remaining` 
  and `Retry-After` headers for better client-side handling.

### Bug fixes

- Resolved an issue where deleted devices continued to appear in the 
  Devices list for up to 30 minutes after deletion.
- Fixed incorrect pagination on the Alerts list when more than 500 
  alerts were active simultaneously.

### Known issues

- Alert escalation emails may not be delivered if the recipient's mail 
  server applies aggressive spam filtering. Whitelist `alerts@siteedge.io` 
  to resolve this.