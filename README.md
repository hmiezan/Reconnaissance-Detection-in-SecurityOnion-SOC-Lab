# Reconnaissance-Detection-in-SecurityOnion-SOC-Lab
This lab demonstrates end‑to‑end visibility of network reconnaissance activity between a Kali attacker and an Active Directory server within a Security Onion 2.4 environment. The goal was to validate IDS/IPS detection and Zeek metadata correlation.

### 1. Lab Architecture

- Attacker	Kali Linux (10.161.170.22)
- Target	Windows Server AD (10.161.90.90)
- SOC Platform	Security Onion 2.4 running Zeek + Suricata + Elastic Stack
- Interface	ens19 (mirrored traffic from Proxmox bridge)
- Tools Used	Nmap, Ping, Security Onion Dashboard

<img width="628" height="453" alt="Ntw Top" src="https://github.com/user-attachments/assets/aee95c98-0dfa-40e1-a55d-6d46413feeeb" />


### 2. Attact Simulation
I executed two reconnaissance techniques from Kali:
- ping 10.161.90.90 > ICMP Discovery
- nmap -sS 10 > TCP SYN port Scan
  
here is teh Attack Flow Diagram (Kill Chain Stage: Reconnaissance)
<img width="682" height="412" alt="attack flow" src="https://github.com/user-attachments/assets/b4ccf4ee-43d9-484a-bac0-c06706ae590d" />

Purpose: identify live hosts and enumerate exposed services on the AD server

### 3. Detecion Result
Security Onion generated multiple alerts confirming detection of reconnaissance activity
<img width="1199" height="259" alt="Detection" src="https://github.com/user-attachments/assets/958e2190-b976-4d4c-aefa-c796e438287f" />

### 4. Analysis and Interpretation
The combination of Suricata alerts and Zeek logs indicates:
The attacker (Kali) performed host discovery (ICMP).
Followed by service enumeration (Nmap SYN scan).
Multiple high‑value AD services were exposed (Kerberos, LDAP, SMB, RPC).
The SOC successfully detected and logged all reconnaissance steps.
This mirrors real‑world adversary behavior in the early stages of an intrusion.

### 5. Outcome
This exercise validated full SOC visibility from packet capture to alert generation.
It confirmed that the mirrored interface (ens19) and IDS configuration are functioning correctly.
The SOC can now detect reconnaissance activity — the first stage of the cyber kill chain.

### 6. Skills Demonstrated
- Network traffic analysis
- IDS/IPS alert interpretation
- Zeek log correlation
- Security Onion 2.4 configuration
- Cyber Kill Chain mapping
- SOC documentation & reporting

### 7. Next Steps(Planned)
- SMB enumeration detection
- Kerberos brute‑force detection
- Lateral movement visibility
- Custom Zeek scripts for enhanced protocol logging
- Full incident response workflow documentation
