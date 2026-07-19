# SOC Home Lab: Attack Simulation & Endpoint Investigation

## Project Overview

This project demonstrates the design and implementation of an isolated Security Operations Center (SOC) home lab used to simulate a real-world endpoint compromise and investigate the resulting malicious activity.

The lab consists of a Windows 10 victim machine and a Kali Linux attacker connected through an isolated internal network. Splunk Enterprise was configured as the Security Information and Event Management (SIEM) platform, while Sysmon provided detailed endpoint telemetry for investigation.

To generate realistic attack data, a controlled malicious payload was hosted on the Kali Linux system and executed on the Windows endpoint. This established a Meterpreter reverse TCP session, allowing simulated attacker activity. Using Splunk and Sysmon, the investigation reconstructed the attack timeline, correlated related process creation events, identified indicators of compromise (IOCs), and validated that endpoint telemetry accurately captured the malicious behavior.

This project demonstrates practical experience with attack simulation, Windows endpoint investigations, SIEM analysis, log correlation, and incident documentation within a controlled lab environment.

## Lab Architecture

<img width="1383" height="834" alt="41- Diagram" src="https://github.com/user-attachments/assets/04e2dd0e-0ff8-4b78-bf2a-6bcbab792f19" />

The home lab consists of a Windows 10 endpoint and a Kali Linux attacker connected through an isolated VirtualBox internal network. Kali Linux hosts and delivers a simulated malicious payload while simultaneously acting as the command-and-control (C2) server. The Windows endpoint collects detailed endpoint telemetry using Sysmon, which is forwarded to Splunk Enterprise through the Universal Forwarder. This architecture enables safe attack simulation, centralized log collection, and end-to-end investigation of malicious activity within a controlled SOC environment.

### Attack Flow

1. Kali Linux hosts the malicious payload and prepares the reverse TCP listener.
2. The Windows endpoint downloads and executes the simulated malicious executable.
3. A Meterpreter reverse TCP session is established.
4. Sysmon records process creation, network connections, and related endpoint events.
5. Splunk ingests the telemetry for centralized analysis.
6. The investigation correlates endpoint artifacts to reconstruct attacker activity and identify indicators of compromise.

