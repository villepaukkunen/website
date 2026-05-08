---
title: My bare metal Kubernetes homelab - or what this website is running on
date: 2026-05-08
---
![Homelab](20260410_173937.jpg)

#### Network Diagram
{{< mermaid >}}
graph
    WAN[WAN] --> ROUTER[pfSense]
    ROUTER --> MAINSWITCH[HPE OfficeConnect Switch 1820 48G J9981A]
    MAINSWITCH --> VLAN1[LAN]
    MAINSWITCH --> VLAN2[NAS]
    MAINSWITCH --> VLAN3[Servers]
    MAINSWITCH --> VLAN4[Personal Devices]
    MAINSWITCH --> VLAN5[IoT Devices]
    VLAN2 --> M73-1[m73-server-1]
    M73-1 --> DAS[Icy Box IB-RD3640SU3 HDD Enclosure]
    VLAN3 --> K3S_SERVERS[K3s Servers]
    VLAN3 --> K3S_AGENTS[K3s Agents]
    K3S_SERVERS --> M73-2[m73-server-2]
    K3S_SERVERS --> M73-3[m73-server-3]
    K3S_SERVERS --> M720q-1[m720q-server-1]
    K3S_AGENTS --> ACER[acer-server-1]
    K3S_AGENTS --> M600-2[m600-server-2]
    VLAN4 --> AP[Zyxel Access Point]
    AP -.-> WLDEV[Wireless Devices]
{{< /mermaid >}}

## Hardware
### Router
- pfSense
	- HP Prodesk 600 G3 SFF
		- Intel® Core™ i3-7100 CPU @ 3.90GHz
		- 16 GB DDR4
		- 128 GB SSD
		- 1 Gbe on board
		- 1 Gbe TP-Link TG-3468 v3.0
		- 2.5 Gbe Intel I226

### NAS
- m73-server-1
	- Lenovo Thinkcentre M73 Tiny
		- Intel® Core™ i3-4150T CPU @ 3.00GHz
		- 12 GB DDR3
		- 128 GB SSD
		- 1 Gbe on board
		- Icy Box IB-RD3640SU3 4 Bay USB HDD Enclosure

### K3s Servers
- m73-server-2
- m73-server-3
	- Lenovo Thinkcentre M73 Tiny
		- Intel® Core™ i3-4150T CPU @ 3.00GHz
		- 12 GB DDR3
		- 128 GB SSD
		- 1 Gbe on board
- m720q-server-1
	- Lenovo Thinkcentre M720q Tiny
		- Intel® Core™ i5-8400T CPU @ 1.70GHz
		- 16 GB DDR4
		- 256 GB SSD
		- 1 Gbe on board

### K3s Agents
- acer-server-1
	- Acer Aspire V5-552G
		- AMD A10-5757M
		- 8 GB DDR3
		- 120 GB SSD
		- 1 Gbe on board
- m600-server-2
	- Lenovo Thinkcentre M600 Tiny
		- Intel® Celeron™ N3010 CPU @ 1.04GHz
		- 4 GB DDR3
		- 16 GB SSD
		- 1 Gbe on board