---
title: User Manual: Modbus TCP
description: End-to-end installation and configuration guide for industrial networking.
---

## 1. Introduction

### 1.1 Purpose
The Modbus TCP Connector connects various industrial devices via the Modbus TCP protocol to the Industrial Edge system. It provides a unified data interface for reading and writing tag values, reducing development effort for modular software solutions.

### 1.2 Scope
This documentation covers the installation and configuration of the Modbus TCP Connector on Industrial Edge Devices (IE Devices), including data type mapping, migration from legacy versions, and performance results.

### 1.3 Target Audience
This manual is intended for Industrial Edge app developers and users who need to integrate Modbus-compatible PLC data into their analytic or visualization applications.

---

## 2. Getting Started

### 2.1 Prerequisites
- **IE Device-OS:** 2.1 or later.
- **Common Configurator:** V2.0 or later.
- **Resource Requirements:** At least 10 GB available hard disk and 2 GB RAM.
- **Browser:** Google Chrome Version 72 or later.

### 2.2 Installation / Access
The installation of an Industrial Edge app follows a standardized three-step process:

1. **Copying from Hub:** Transfer the Modbus TCP Connector from the Industrial Edge Hub Library to your IEM catalog.
2. **Installing on Device:** Open the IEM catalog, select the app, and click "Install" for your target IE Device.
3. **Starting the App:** Log in to the IE Device home page, open the "Apps" tab, and launch the **Common Configurator**.

!!! abstract "Generic Installation Walkthrough"
    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
        <iframe src="https://players.brightcove.net/1813624294001/f83fb7f6-75c0-411c-872c-ab6095a19211_default/index.html?videoId=6338443126112" 
                allowfullscreen 
                webkitallowfullscreen 
                mozallowfullscreen 
                style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;"></iframe>
    </div>

---

## 3. Key Concepts

The Modbus TCP Connector is part of the **Connectivity Suite (CS)**, which enables direct integration with the Industrial Information Hub (IIH). 

![Architecture Overview](architecture-overview.svg)

### Connectivity Suite Benefits
- **Direct Integration:** Tag values are available directly in the IIH without mandatory Databus configuration.
- **Data Normalization:** Translates Modbus-specific registers into standardized Industrial Edge data types.
- **Performance:** Version 4.0+ uses gRPC for high-speed data transfer compared to legacy MQTT-based versions.

---

## 4. How to Use (Core Tasks)

### 4.1 Managing Data Sources
**Goal:** Define and connect to a Modbus TCP Server/PLC.

1. Navigate to **Get Data > Connector Configuration** in the Common Configurator.
2. Select **Modbus TCP Connector**.
3. Click **Add data source** and enter the PLC IP address and connection details.

![Connection Flow](iec-flow.svg)

### 4.2 Adding Tags
**Goal:** Define specific register addresses to subscribe to.

1. Open the **Tags** tab and select your configured data source.
2. Click **Add tag**.
3. Enter the **Address** (e.g., `40001` for a holding register) and select the **Data Type**.
4. Use dot notation for Raw data blocks (e.g., `address.length`).

---

## 5. Advanced Configuration

### 5.1 Supported Data Types

| Data Type | Description | Max Length |
| :--- | :--- | :--- |
| **Bool** | 1 bit | - |
| **Int/UInt** | Signed/Unsigned integer (2 bytes) | - |
| **DInt/UDInt** | Signed/Unsigned integer (4 bytes) | - |
| **Real/LReal** | Floating point (4/8 bytes) | - |
| **String** | Character string | 250 chars |
| **Raw** | Continuous register memory area | Defined by length |

---

## 6. Troubleshooting

| Issue | Possible Cause | Solution |
| :--- | :--- | :--- |
| **Data not updating** | Acquisition cycle too slow or "On Progress" flag not set. | Verify the acquisition mode settings in Common Configurator. |
| **Invalid Address** | Incorrect register range or formatting. | Check the Modbus server documentation for valid address ranges. |
| **Memory Error** | Configuration file too large for device limits. | Upgrade to IE Device version 1.21+ to support Memory Management. |

---

## 7. Glossary

- **Connectivity Suite (CS):** A standardized communication layer for Industrial Edge.
- **IIH:** Industrial Information Hub.
- **IEM:** Industrial Edge Management.
- **PLC:** Programmable Logic Controller.