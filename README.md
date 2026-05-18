# Reconnaissance-Detection-in-SecurityOnion-SOC-Lab
This lab demonstrates end‑to‑end visibility of network reconnaissance activity between a Kali attacker and an Active Directory server within a Security Onion 2.4 environment. The goal was to validate IDS/IPS detection and Zeek metadata correlation.

### 1. Environment Setup

- Attacker	Kali Linux (10.161.170.22)
- Target	Windows Server AD (10.161.90.90)
- SOC Platform	Security Onion 2.4 running Zeek + Suricata + Elastic Stack
- Interface	ens19 (mirrored traffic from Proxmox bridge)
- Tools Used	Nmap, Ping, Security Onion Dashboard

### 2. Attact Simulation
The attacker performed ICMP reconnaissance followed by a TCP SYN scan to enumerate open ports on the AD server.
- ping 10.161.90.90
- nmap -sS 10.161.90.90

### 3. Detecion Result
Summarize the alerts captured
<img width="1199" height="259" alt="Detection" src="https://github.com/user-attachments/assets/958e2190-b976-4d4c-aefa-c796e438287f" />

### 4. Analysis and Interpretation
Suricata correctly classified reconnaissance traffic as suspicious inbound scans.
Zeek enriched metadata with ICMP and TCP SYN connection details.
Elastic Search indexed the events for visualization in the Security Onion dashboard.

### 5. Outcome and Learning
This exercise validated full SOC visibility from packet capture to alert generation.
It confirmed that the mirrored interface (ens19) and IDS configuration are functioning correctly.
The SOC can now detect reconnaissance activity — the first stage of the cyber kill chain.
