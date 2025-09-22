# Network-Automation-PoC



\# Network Automation Proof of Concept (PoC)

\## MN521 - Network Automation Group Project



This repository contains Ansible playbooks and configurations for automating network operations in a multi-vendor environment .



\## Project Overview

This Proof of Concept demonstrates network automation using Ansible to manage:

\- VLAN configurations on Cisco switches

\- OSPF routing on Cisco routers

\- BGP peering with external ISP

\- Access Control Lists (ACLs) on Cisco routers

\- Firewall policies on Juniper SRX



\## Topology

The network topology consists of:

\- 2x Cisco Switches (IOSvL2)

\- 4x Cisco Routers (IOSv) 

\- 1x Juniper SRX Firewall (vSRX)

\- 1x Ubuntu Controller (Ansible host)

\- External ISP Router



\## Prerequisites

\- Ansible 2.9+

\- Python 3.8+

\- Network devices accessible via SSH

\- Required Ansible collections:

&nbsp; - `ansible-galaxy collection install cisco.ios`

&nbsp; - `ansible-galaxy collection install junipernetworks.junos`



\## Repository Structure

Network-Automation-PoC/

├── inventories/

│ └── production.yml # Device inventory

├── playbooks/ # Main playbooks

│ ├── vlan\_config.yml

│ ├── ospf\_config.yml

│ ├── bgp\_config.yml

│ ├── acl\_config.yml

│ └── firewall\_config.yml

├── templates/ # Configuration templates

│ ├── switch\_base.j2

│ ├── router\_base.j2

│ └── firewall\_base.j2

├── vars/ # Variable files

│ ├── common\_vars.yml

│ ├── vlan\_vars.yml

│ ├── ospf\_vars.yml

│ ├── bgp\_vars.yml

│ └── security\_vars.yml

├── group\_vars/ # Group-specific variables

│ ├── all.yml

│ ├── switches.yml

│ ├── routers.yml

│ └── firewall.yml

├── host\_vars/ # Host-specific variables

│ ├── switch-1.yml

│ ├── router-1.yml

│ └── srx-firewall.yml

├── docs/ # Documentation

│ └── screenshots/

└── README.md



\## Quick Start



1\. \*\*Clone the repository:\*\*

git clone https://github.com/robenbhandari/Network-Automation-PoC



Install required collections:



ansible-galaxy collection install cisco.ios

ansible-galaxy collection install junipernetworks.junos



Configure inventory:

Update inventories/production.yml with your device IP addresses and credentials.



Run a playbook:

ansible-playbook -i inventories/production.yml playbooks/vlan\_config.yml



Creates VLANs 10 (SALES) and 20 (HR)



Configures access ports and trunk links



OSPF Configuration

ansible-playbook -i inventories/production.yml playbooks/ospf\_config.yml

Configures OSPF on all routers in Area 0



Advertises connected networks



BGP Configuration

ansible-playbook -i inventories/production.yml playbooks/bgp\_config.yml

Establishes eBGP peering between Router-1 and ISP



Advertises internal networks



ACL Configuration

ansible-playbook -i inventories/production.yml playbooks/acl\_config.yml

Applies ACL to block VLAN 20 internet access



Permits all other traffic



Firewall Configuration

ansible-playbook -i inventories/production.yml playbooks/firewall\_config.yml

Configures security zones and policies



Blocks inbound ICMP from internet



Device Credentials

Credentials are stored in group\_vars/all.yml. For production use, consider using Ansible Vault:





ansible-vault create group\_vars/all.yml

Testing

After running playbooks, verify configurations:





\# Test connectivity

ansible routers -i inventories/production.yml -m ping



\# Gather facts

ansible-playbook -i inventories/production.yml playbooks/gather\_facts.yml

Contributing

Fork the repository



Create a feature branch



Commit your changes



Push to the branch



Create a Pull Request



Group Members

Rabin Bhandari



Bipin Giri



Amrit Adhikari



Binay Shrestha



License

MIT License







