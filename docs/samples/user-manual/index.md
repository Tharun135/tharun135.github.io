# End-User Manual: SIMATIC S7+ Connector

This is a sample interactive end-user manual created dynamically from an uploaded PDF. It demonstrates the use of **Admonitions**, **Tables**, **Tabs**, and **Code Blocks** common in modern technical documentation.

---

## 1. Introduction to SIMATIC S7+ Connector

Welcome to the SIMATIC S7+ Connector documentation for Industrial Edge.

The SIMATIC S7+ Connector is a south-bound connector that connects data from S7-1200/1500 PLCs, PLCSim Advanced, and Siemens Software Controller with Industrial Edge. Connectors are essential to collect data from various PLCs and devices and make it available on the Industrial Edge system. 

With the S7+ Connector, data can be accessed via the optimized S7 protocol. This connector is developed as a Connectivity Suite Connector and therefore supports standardized configuration as well as data transfer.

!!! tip "Common Configurator"
    The Common Configurator configures the Connector and is available free of charge in the Industrial Edge Marketplace.

### Security Information

Siemens provides products and solutions with industrial cybersecurity functions that support the secure operation of plants, systems, machines, and networks.

!!! danger "Unauthorized Access"
    Customers are responsible for preventing unauthorized access to their plants, systems, machines and networks. Systems should only be connected to an enterprise network or the internet if appropriate security measures (e.g., firewalls and network segmentation) are in place.

!!! warning "Product Updates"
    Siemens strongly recommends that product updates are applied as soon as they are available. Failure to apply the latest updates may increase customer's exposure to cyber threats.

---

## 2. Requirements and Time Synchronization

Both the PLC and the Industrial Edge (IE) Device must use time synchronization (for example, NTP). Without synchronization, the times of the two devices become out of sync.

### Firmware Minimum Requirements

To configure the PLC time stamp, you must meet the following firmware versions:

=== "S7-1500"
    - **Minimum Firmware:** V2.6 
    - **Required Software:** TIA Portal V15.1 or newer

=== "S7-1200"
    - **Minimum Firmware:** V4.4 
    - **Required Software:** TIA Portal V16 or newer

---

## 3. Supported Data Types

Data Types from a PLC must be implicitly converted in order to use them in an IE Device. The data types are converted from S7-1500/1200 PLC data types to Connectivity Suite Data Types, and then into the corresponding Industrial Edge Data Types.

| S7-1500/1200 Type | Connectivity Suite Type | Length (bits) | Edge Data Type | JSON Value Type |
| :--- | :--- | :--- | :--- | :--- |
| **Bool** | Bool | 1 | Bool | Integer |
| **Byte** | UInt8 | 8 | USInt | Integer |
| **Word** | UInt16 | 16 | UInt | Integer |
| **DWord** | UInt32 | 32 | UDInt | Integer |
| **LWord** | UInt64 | 64 | ULInt | String |
| **SInt** | Int8 | 8 | SInt | Integer |
| **Real** | Float32 | 32 | Real | Floating-point |
| **String** | String | 8 (per char) | String | String |

!!! info "About Array Support"
    Arrays are provided in the Common Configurator as a single tag. SIMATIC S7+ Connector supports arrays of default data types, including `String`, `WString` and `DTL`. It provides all individual elements of an array as separate tags and also the whole array as one common tag in a JSON file.

---

## 4. Configuring the PLC Time Stamp

All tags receive a time stamp. You can activate the PLC time stamp (Source Timestamp) or use the connector time stamp for subscribed tags. 

| Parameter | Value | Description |
| :--- | :--- | :--- |
| `use_source_timestamp` | `True` / `False` | Activates the PLC time stamp. |
| `max_source_timestamp_diff` | `Int` | The maximum acceptable differential value in seconds. <br/> - **0 sec**: the difference is not checked. PLC time is used. <br/> - **n sec**: when the difference between PLC and connector exceeds `n`, the local time stamp is used. |

!!! caution "Alarm Timestamps vs Data Subscriptions"
    When configuring both data subscriptions and alarm subscriptions, it is strongly recommended to enable **"Source Timestamp"** for your data subscriptions. Alarm timestamps are always generated and provided by the PLC. Using the Source Timestamp ensures a unified and accurate timeline across all your subscribed information.