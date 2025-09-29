---

# Network-Automation-PoC

## MN521 - Network Automation Group Project

This repository contains **Ansible playbooks, configuration templates, and variables** designed to automate network operations across a **multi-vendor hybrid environment**. The Proof of Concept (PoC) showcases how infrastructure teams can reduce manual effort, minimize errors, and standardize configurations using modern automation practices.

---

## 🔹 Project Overview

The objective of this PoC is to demonstrate how **Ansible** can be leveraged for end-to-end automation of common network tasks in a mixed-vendor environment. The implementation focuses on:

* **Cisco Switches (IOSvL2)** – Automating VLAN configuration and trunk/access assignments.
* **Cisco Routers (IOSv)** – Automating OSPF and BGP configuration, ACLs, and edge routing.
* **Juniper SRX (vSRX)** – Automating firewall policy and zone configuration.
* **Controller Node (Ubuntu)** – Hosting Ansible, inventory, and playbooks.

Key capabilities demonstrated include:

✅ Automated VLAN creation and port assignment
✅ OSPF routing configuration across multiple routers in Area 0
✅ BGP peering with an external ISP router
✅ ACL deployment to restrict VLAN 20’s internet access
✅ Juniper firewall security zone and policy automation

This project validates how **multi-vendor automation** reduces configuration drift, increases repeatability, and accelerates deployment times in enterprise-grade environments.

---

## 🔹 Network Topology

The PoC lab is designed to replicate a small-scale enterprise network with external ISP connectivity.

**Components:**

* **2× Cisco Switches (IOSvL2)** – Core/distribution VLAN management
* **4× Cisco Routers (IOSv)** – Internal routing, OSPF/BGP operations
* **1× Juniper SRX Firewall (vSRX)** – Internet edge security enforcement
* **1× Ubuntu Controller** – Central automation server running Ansible
* **1× External ISP Router** – BGP peering and simulated internet

> 📌 The topology simulates **LAN, WAN, and security domains** with integrated automation workflows.

---

## 🔹 Prerequisites

Before deploying this PoC, ensure the following:

* **Software & Tools**

  * Ansible **2.9+**
  * Python **3.8+**
  * Git installed on controller node

* **Ansible Collections**

  ```bash
  ansible-galaxy collection install cisco.ios
  ansible-galaxy collection install junipernetworks.junos
  ```

* **Connectivity**

  * All network devices must be **reachable via SSH**
  * Proper user credentials configured in inventory or stored securely in **Ansible Vault**

---

## 🔹 Repository Structure

```
Network-Automation-PoC/
├── inventories/
│   └── production.yml        # Device inventory (IPs, groups, credentials)
├── playbooks/                # Automation workflows
│   ├── vlan_config.yml       # VLAN creation & port assignments
│   ├── ospf_config.yml       # OSPF deployment
│   ├── bgp_config.yml        # BGP peering with ISP
│   ├── acl_config.yml        # Access control lists
│   └── firewall_config.yml   # Juniper firewall automation
├── templates/                # Jinja2 configuration templates
│   ├── switch_base.j2
│   ├── router_base.j2
│   └── firewall_base.j2
├── vars/                     # Variable definitions
│   ├── common_vars.yml
│   ├── vlan_vars.yml
│   ├── ospf_vars.yml
│   ├── bgp_vars.yml
│   └── security_vars.yml
├── group_vars/               # Group-level variables
│   ├── all.yml
│   ├── switches.yml
│   ├── routers.yml
│   └── firewall.yml
├── host_vars/                # Host-level variables
│   ├── switch-1.yml
│   ├── router-1.yml
│   └── srx-firewall.yml
├── docs/                     # Documentation & evidence
│   └── screenshots/
└── README.md
```

---

## 🔹 Quick Start Guide

### 1. Clone the Repository

```bash
git clone https://github.com/robenbhandari/Network-Automation-PoC
cd Network-Automation-PoC
```

### 2. Install Required Collections

```bash
ansible-galaxy collection install cisco.ios
ansible-galaxy collection install junipernetworks.junos
```

### 3. Configure Inventory

Edit `inventories/production.yml` with device IP addresses, usernames, and passwords.

For production environments, encrypt credentials with **Ansible Vault**:

```bash
ansible-vault create group_vars/all.yml
```

### 4. Run Playbooks

* **VLAN Configuration**

  ```bash
  ansible-playbook -i inventories/production.yml playbooks/vlan_config.yml
  ```

  * Creates VLAN 10 (SALES) and VLAN 20 (HR)
  * Configures access/trunk ports

* **OSPF Configuration**

  ```bash
  ansible-playbook -i inventories/production.yml playbooks/ospf_config.yml
  ```

  * Deploys OSPF in Area 0 across routers
  * Advertises connected networks

* **BGP Configuration**

  ```bash
  ansible-playbook -i inventories/production.yml playbooks/bgp_config.yml
  ```

  * Establishes **eBGP peering** with ISP router
  * Advertises enterprise internal networks

* **ACL Configuration**

  ```bash
  ansible-playbook -i inventories/production.yml playbooks/acl_config.yml
  ```

  * Blocks **VLAN 20 internet access**
  * Permits all other traffic

* **Firewall Configuration**

  ```bash
  ansible-playbook -i inventories/production.yml playbooks/firewall_config.yml
  ```

  * Creates Juniper **security zones**
  * Enforces inbound ICMP block from internet

---

## 🔹 Testing & Verification

* **Ping Test**

  ```bash
  ansible routers -i inventories/production.yml -m ping
  ```

* **Gather Device Facts**

  ```bash
  ansible-playbook -i inventories/production.yml playbooks/gather_facts.yml
  ```

* **Manual Verification**

  * Use `show running-config` on devices
  * Validate VLANs, OSPF neighbors, BGP sessions, ACLs, and firewall rules

---

## 🔹 Contribution Workflow

1. Fork the repository
2. Create a feature branch (`feature/my-feature`)
3. Commit changes with clear messages
4. Push changes and open a Pull Request

---

## 🔹 Group Members

* **Rabin Bhandari**
* **Bipin Giri**
* **Amrit Adhikari**
* **Binay Shrestha**
* **James Nepal**

---

## 🔹 License

This project is licensed under the **MIT License**. You are free to use, modify, and distribute with attribution.

## commit by Amrit
* **mit251172@stud.mit.edu.au**