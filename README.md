# Exercise 2 – Demonstrate NFV with pfSense

This document provides a clean, GitHub‑ready version of **Exercise 2** from the Cloud Networking Concepts lab. It is formatted in Markdown for easy inclusion in repositories.

---

## Overview

Network Function Virtualization (NFV) replaces traditional hardware appliances with virtualized network services. In this exercise, **pfSense** acts as a virtual router and firewall, demonstrating NFV capabilities such as:

* Creating firewall rules
* Managing WAN/LAN interfaces
* Configuring routing
* Setting up NAT

Devices used:

* **ACIDC01** – Windows Server 2022 (192.168.0.1/24)
* **ACIPFSENSE** – pfSense v2.7.2 Virtual Router (192.168.0.5/24)

---

# Task 1 – Configure pfSense Firewall Rules

## Objective

Configure pfSense WAN firewall rules to:

* Allow remote access to the pfSense management interface
* Allow remote ping to the LAN interface

---

## Step‑by‑Step Instructions

### **1. Access pfSense from ACIDC01**

1. Open **Microsoft Edge** on ACIDC01.

2. Navigate to:

http://192.168.0.5 (192.168.0.5 in Bing)


### **2. Log in to pfSense**

Use the following credentials:

Username: admin
Password: Passw0rd


---

## 3. Configure WAN Firewall Rules

### **Rule 1 – Allow Web Management Access (HTTP)**

1. In pfSense, go to: **Firewall → Rules → WAN**
2. Select **Add** (arrow up icon – add to top).
3. Configure:
   * **Action:** Pass
   * **Interface:** WAN
   * **Protocol:** TCP
   * **Destination Port Range:** HTTP (80)
   * **Description:** Allow HTTP management access
4. Click **Save**, then **Apply Changes**.

### **Rule 2 – Allow ICMP (Ping) to LAN Interface**

1. Still under **WAN rules**, select **Add** again.
2. Configure:
   * **Action:** Pass
   * **Interface:** WAN
   * **Protocol:** ICMP
   * **ICMP Type:** Echo Request
   * **Description:** Allow ping to LAN interface
3. Click **Save**, then **Apply Changes**.

---

# Task 2 – Create a LAN Interface in pfSense

### **1. Navigate to Interfaces**

Go to: **Interfaces → Assignments**

### **2. Add a New LAN Interface**

1. Select **Add** to create a new interface.
2. Assign the interface to the appropriate NIC.
3. Click the new interface name (e.g., OPT1) to configure it.
4. Set:
   * **Enable Interface:** ✔
   * **IPv4 Configuration Type:** Static IPv4
   * **IPv4 Address:** `192.168.1.1/24`
5. Click **Save**, then **Apply Changes**.

---

# Task 3 – Configure Local Route Table

### **1. Navigate to Routing**

Go to: **System → Routing → Gateways**

### **2. Add a Static Route**

1. Select **Static Routes** tab.
2. Click **Add**.
3. Configure:
   * **Destination Network:** (example) `10.10.10.0/24`
   * **Gateway:** Select the appropriate gateway
4. Save and apply.

---

# Task 4 – Configure NAT on pfSense

### **1. Navigate to NAT Settings**

Go to: **Firewall → NAT → Outbound**

### **2. Set NAT Mode**

Choose one of the following:

* **Automatic Outbound NAT** (recommended for beginners)
* **Hybrid Outbound NAT** (allows custom rules)

### **3. Add a NAT Rule (if using Hybrid/Manual)**

1. Click **Add**.
2. Configure:
   * **Interface:** WAN
   * **Source:** LAN subnet
   * **Translation:** Interface Address
3. Save and apply.

---

# Summary

By completing this exercise, I have:

* Accessed and authenticated into pfSense
* Configured WAN firewall rules for management and ICMP
* Created and configured a LAN interface
* Added static routes to the routing table
* Configured NAT for outbound traffic

This demonstrates how pfSense functions as an NFV platform, replacing traditional hardware firewalls and routers with flexible, virtualized network services.

---
