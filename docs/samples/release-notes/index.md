---
title: Release Notes
description: Changelogs and evolutionary updates for technical assets.
---

This is a sample release notes page formatted according to standard software changelog templates. It incorporates factual context automatically generated from the **SIMATIC S7+ Connector** and **IIH Essentials API** documentation.

---

## Version 2.4.0 – February 2026

### New Features
* **Anchor Assets Support**: Added full CRUD operations for Anchor Assets, Anchor Types, and Anchor Attributes via the IIH Essentials API.
* **Data Backup & Restore**: Introduced new endpoints (`GET /DataService/Backup` and `POST /DataService/Restore`) for full configuration portability.

### Enhancements
* **Improved API Response Speed**: Optimized the `GET /DataService/Adapters` endpoint, increasing parsing speed by ~30% for systems with over 100+ connected sources.
* **Disk Space Reporting**: Extended disk space reporting metrics to include granular details for Aggregations, Aspects, and DataRetentions.

### Bug Fixes
* **Large File Uploads**: Fixed an issue where multipart file uploads failed for large configuration backups exceeding 16 MB.
* **Alarm Synchronization**: Resolved an issue where acknowledged and deleted status of alarms were not properly reflected in the Databus Gateway.

### Breaking Changes
* **Property Renaming**: The property `$anchor` in the `AggregationValue` schema has been officially renamed to `$pointer`.
* **Deprecated Legacy Endpoint**: The legacy `/analyze-text` API endpoint has been fully removed. 
   &rarr; *Use `/DataService/Calculate` instead.*

---

## Version 2.3.0 – January 2026

### New Features
* **Central Configuration**: The SIMATIC S7+ Connector can now be completely configured remotely from a central Common Configurator running on the IEM System.
* **Array Support**: Added comprehensive reading and writing capabilities for arrays of default data types, including `String`, `WString`, and `DTL`.

### Enhancements
* **Cyclic Continuous Mode**: Added support for the `Cyclic Continuous` acquisition mode on S7+ tags for higher frequency data streaming.
* **Reduced Memory Footprint**: Decreased the local storage footprint of the CS Databus Gateway by optimizing JSON generation routines.

### Bug Fixes
* **Negative Array Bounds**: Fixed browsing failures for tags with negative array bounds in the S7-1500 Software Controller.
* **String Allocation Failure**: Fixed a writing failure that sporadically occurred when processing large `String`-arrays in Edge.
