# 🎓 Albion University Enterprise Network Design

## 📄 Project Description
This project demonstrates the **design and simulation of a scalable enterprise network** for **Albion University**.  
The scenario involves connecting **two geographically separated campuses** (Main Campus and Branch Campus) while ensuring:

- Logical separation of departments  
- Secure access control  
- Reliable internal and external connectivity  

The solution follows a **Hierarchical Network Design Model** (Core, Distribution, Access) and supports multiple faculties, administrative departments, and centralized services.

---

## 🛠️ Tools & Technologies Used

### 🔧 Simulation Software
- **Cisco Packet Tracer**

### 🖥️ Hardware Models Simulated
- **Routers:** Cisco 2911 (ISR) – WAN connectivity  
- **Layer 3 Switches:** Cisco 3560 / 3650 – Inter-VLAN routing  
- **Layer 2 Switches:** Cisco 2960 – Access layer  

### 🌐 Protocols & Services
- **Routing:** RIPv2 (Internal), Static Routing (External)
- **Switching:** VLANs (802.1Q), Trunking, STP
- **Services:** DHCP, DNS, HTTP, FTP
- **WAN:** Serial DCE/DTE connections

---

## 📋 Tasks & Objectives

### 1️⃣ Planning & Topology Design
- **Requirement Analysis:**  
  - Building A: Admin, HR, Finance, Business  
  - Building B: Engineering, Art & Design  
  - Building C: Student Labs, IT Department  
  - Branch Campus: Health Sciences  
- **Hierarchical Design:** Core–Distribution–Access architecture for scalability  
- **IP Addressing Scheme:**  
  - Subnetting using `192.168.x.0/24`  
  - VLAN IDs mapped directly to subnets for easier management  

---

### 2️⃣ Configuration & Implementation
- **VLAN Segmentation:** Separate VLANs per department to isolate broadcast domains  
- **Inter-VLAN Routing:**  
  - Layer 3 switching  
  - Router-on-a-Stick implementation  
- **Dynamic IP Addressing:**  
  - Router-based DHCP pools for end devices  
- **Routing Protocols:**  
  - RIPv2 for inter-campus routing  
  - Static routes for external Cloud Email Server  

---

### 3️⃣ Testing & Verification
- Verified end-to-end connectivity using **Ping** and **PDU simulation**
- Confirmed access to:
  - Internal Web Server
  - External Cloud Email Server

---

## 🏗️ Network Architecture

### VLAN & IP Addressing Table

| Department        | Location            | VLAN ID | Network Address     | Gateway        |
|------------------|---------------------|--------:|---------------------|----------------|
| Admin            | Main – Bldg A       | 10      | 192.168.1.0/24      | 192.168.1.1    |
| HR               | Main – Bldg A       | 20      | 192.168.2.0/24      | 192.168.2.1    |
| Finance          | Main – Bldg A       | 30      | 192.168.3.0/24      | 192.168.3.1    |
| Business         | Main – Bldg A       | 40      | 192.168.4.0/24      | 192.168.4.1    |
| Engineering      | Main – Bldg B       | 50      | 192.168.5.0/24      | 192.168.5.1    |
| Art & Design     | Main – Bldg B       | 60      | 192.168.6.0/24      | 192.168.6.1    |
| Student Lab      | Main – Bldg C       | 70      | 192.168.7.0/24      | 192.168.7.1    |
| IT Department    | Main – Bldg C       | 80      | 192.168.8.0/24      | 192.168.8.1    |
| Health Staff     | Branch Campus       | 90      | 192.168.9.0/24      | 192.168.9.1    |
| Health Lab       | Branch Campus       | 100     | 192.168.10.0/24     | 192.168.10.1   |

---

## ⚙️ Key Configuration Snippets

###  VLAN Configuration (Switch)
- enable
- configure terminal
- vlan 10
 - name ADMIN
- vlan 20
 - name HR
- exit
---
## Router-on-a-Stick (Inter-VLAN Routing)

This configuration enables the router to handle traffic between different VLANs by using sub-interfaces. This specific block sets up the default gateway for the **Admin Department** (VLAN 10).

### Configuration Commands

```bash
interface g0/0.10
 description Gateway for ADMIN
 encapsulation dot1Q 10
 ip address 192.168.1.1 255.255.255.0
```


## DHCP Pool Configuration

This configuration sets up the router to act as a DHCP server, automatically assigning IP addresses to devices within the VLAN 10 network.

### Configuration Commands

```bash
ip dhcp pool VLAN_10_POOL
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 8.8.8.8
```
## RIPv2 Routing Configuration

This section configures the Routing Information Protocol (RIP) Version 2 to allow dynamic route exchange between routers.

### Configuration Commands

```bash
router rip
 version 2
 network 192.168.1.0
 network 10.10.10.0
 no auto-summary
```
