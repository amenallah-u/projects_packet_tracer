# ⚙️ Configuration Files & Scripts - TechGlobal Solutions

This folder contains all the Command Line Interface (CLI) scripts and graphical configurations used to build the **TechGlobal Solutions Multi-Site Network** in Cisco Packet Tracer.

**Module:** Virtualisation Réseau
**Supervisor:** Pr. Bilel Hamdi

---

## 📋 Table of Contents
1. [Switch_A (Site A)](#1-switch_a-site-a)
2. [Switch_B (Site B)](#2-switch_b-site-b)
3. [Router_A (Site A - HQ)](#3-router_a-site-a-hq)
4. [Router_B (Site B - Branch)](#4-router_b-site-b-branch)
5. [Router_ISP (Internet Simulation)](#5-router_isp-internet-simulation)
6. [Server Configurations (Data Centers)](#6-server-configurations-data-centers)

---

## 1. Switch_A (Site A)

```cisco
enable
configure terminal
hostname Switch_A

! Creation of VLANs
vlan 10
 name Administration
vlan 20
 name Finance
vlan 30
 name IT
vlan 40
 name Guest
vlan 50
 name DataCenter
exit

! Access Ports Assignment
interface range fa0/1-3
 switchport mode access
 switchport access vlan 10
interface range fa0/4-6
 switchport mode access
 switchport access vlan 20
interface fa0/7
 switchport mode access
 switchport access vlan 30
interface fa0/8
 switchport mode access
 switchport access vlan 40
interface fa0/9
 switchport mode access
 switchport access vlan 10
interface fa0/10
 switchport mode access
 switchport access vlan 10

! Trunk Link to Router_A
interface fa0/24
 switchport mode trunk
 switchport trunk allowed vlan all
end
write memory