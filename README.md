# SOC Home Lab: Attack Simulation & Endpoint Investigation

## Project Overview

This project demonstrates the design and implementation of an isolated Security Operations Center (SOC) home lab used to simulate a real-world endpoint compromise and investigate the resulting malicious activity.

The lab consists of a Windows 10 victim machine and a Kali Linux attacker connected through an isolated internal network. Splunk Enterprise was configured as the Security Information and Event Management (SIEM) platform, while Sysmon provided detailed endpoint telemetry for investigation.

To generate realistic attack data, a controlled malicious payload was hosted on the Kali Linux system and executed on the Windows endpoint. This established a Meterpreter reverse TCP session, allowing simulated attacker activity. Using Splunk and Sysmon, the investigation reconstructed the attack timeline, correlated related process creation events, identified indicators of compromise (IOCs), and validated that endpoint telemetry accurately captured the malicious behavior.

This project demonstrates practical experience with attack simulation, Windows endpoint investigations, SIEM analysis, log correlation, and incident documentation within a controlled lab environment.
