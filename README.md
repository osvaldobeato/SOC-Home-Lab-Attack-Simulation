# SOC Home Lab: Attack Simulation & Endpoint Investigation

## Project Overview

This project demonstrates the design and implementation of an isolated Security Operations Center (SOC) home lab used to simulate a real-world endpoint compromise and investigate the resulting malicious activity.

The lab consists of a Windows 10 victim machine and a Kali Linux attacker connected through an isolated internal network. Splunk Enterprise was configured as the Security Information and Event Management (SIEM) platform, while Sysmon provided detailed endpoint telemetry for investigation.

To generate realistic attack data, a controlled malicious payload was hosted on the Kali Linux system and executed on the Windows endpoint. This established a Meterpreter reverse TCP session, allowing simulated attacker activity. Using Splunk and Sysmon, the investigation reconstructed the attack timeline, correlated related process creation events, identified indicators of compromise (IOCs), and validated that endpoint telemetry accurately captured the malicious behavior.

This project demonstrates practical experience with attack simulation, Windows endpoint investigations, SIEM analysis, log correlation, and incident documentation within a controlled lab environment.

## Lab Enviroment Architecture

<img width="1383" height="834" alt="41- Diagram" src="https://github.com/user-attachments/assets/04e2dd0e-0ff8-4b78-bf2a-6bcbab792f19" />

The home lab consists of a Windows 10 endpoint and a Kali Linux attacker connected through an isolated VirtualBox internal network. Kali Linux hosts and delivers a simulated malicious payload while simultaneously acting as the command-and-control (C2) server. The Windows endpoint collects detailed endpoint telemetry using Sysmon, which is forwarded to Splunk Enterprise through the Universal Forwarder. This architecture enables safe attack simulation, centralized log collection, and end-to-end investigation of malicious activity within a controlled SOC environment.

### Attack Flow

1. Kali Linux hosts the malicious payload and prepares the reverse TCP listener.
2. The Windows endpoint downloads and executes the simulated malicious executable.
3. A Meterpreter reverse TCP session is established.
4. Sysmon records process creation, network connections, and related endpoint events.
5. Splunk ingests the telemetry for centralized analysis.
6. The investigation correlates endpoint artifacts to reconstruct attacker activity and identify indicators of compromise.

<br>

## Skills Demonstrated

- Built and configured an isolated SOC home lab using VirtualBox.
- Configured Windows endpoint telemetry collection using Sysmon.
- Configured Splunk Enterprise as a centralized SIEM platform.
- Deployed and configured the Splunk Universal Forwarder for log ingestion.
- Simulated a controlled endpoint compromise using Metasploit Framework and Meterpreter.
- Generated and analyzed Windows endpoint telemetry during simulated attacker activity.
- Investigated process creation events using Sysmon Event ID 1.
- Correlated endpoint telemetry to reconstruct the attack timeline.
- Identified Indicators of Compromise (IOCs) from process execution and network activity.
- Conducted log analysis and incident investigation using Splunk Search Processing Language (SPL).
- Documented investigative findings and attack methodology using professional SOC documentation practices.

<br>

## Tools Used

| Tool | Purpose |
|------|---------|
| VirtualBox | Hosted the isolated virtual lab environment |
| Windows 10 | Victim endpoint used during the attack simulation |
| Kali Linux | Attacker machine hosting Metasploit and malicious payload |
| Metasploit Framework | Generated the Meterpreter payload and reverse TCP session |
| Sysmon | Collected detailed endpoint telemetry |
| Splunk Enterprise | Centralized SIEM for log collection and investigation |
| Splunk Universal Forwarder | Forwarded Windows endpoint telemetry to Splunk |
| PowerShell | Assisted with system configuration and administrative tasks |
| Windows Event Logs | Provided endpoint event data for analysis |

<br>

## Investigation Walkthrough

This section documents the complete attack lifecycle, from building the lab environment to simulating malicious activity and investigating the resulting endpoint telemetry in Splunk.

### Phase 1 – Building the SOC Lab

The following steps document the creation of the isolated SOC environment that was used throughout this investigation.

<img width="1920" height="1080" alt="1-Starting with a clean Windows host before building the SOC home lab" src="https://github.com/user-attachments/assets/0b65c88b-2f13-47a9-83ad-8b03cd5881cb" />
Starting with a clean Windows host before building the SOC home lab

<br>

<img width="1920" height="1080" alt="2-Downloading Oracle VirtualBox to create the virtual lab Environment" src="https://github.com/user-attachments/assets/ec327f6c-4fe6-4b8b-949f-a843dbd5f307" />
Downloading Oracle VirtualBox to create the virtual lab Environment
<br>

<img width="1920" height="1080" alt="3-Verified the VirtualBox installer intergrity using SHA256 before installation  This is a great screenshot because it shows security awareness" src="https://github.com/user-attachments/assets/dcd88307-b509-4c4c-b462-31cf540cdb5a" />
Verified the VirtualBox installer intergrity using SHA256 before installation. This is a great screenshot because it shows security awareness
<br>

<img width="1920" height="1080" alt="5-VirtualBox successfully installed and ready to host virtual machines " src="https://github.com/user-attachments/assets/8bd10ee3-1ad6-4f7a-a2ef-63a26d0f82a0" />
VirtualBox successfully installed and ready to host virtual machines
<br>

<img width="1920" height="1080" alt="7-Creating te Windows 10 virtual machine and allocating system resources " src="https://github.com/user-attachments/assets/4eda38bf-0204-4c1a-b5c3-76f64b56f358" />
Creating te Windows 10 virtual machine and allocating system resources
<br>

<img width="1920" height="1080" alt="11-Windows 10 virtual machine successfully deployed" src="https://github.com/user-attachments/assets/65e3d12e-ae12-40d3-a031-48e7a51331d4" />
Windows 10 virtual machine successfully deployed
<br>

<img width="1920" height="1080" alt="13-Successfully built a dual-VM SOC home lab consisting of a Windows endpoint and a Kali Linux attacker machine " src="https://github.com/user-attachments/assets/5d39ab1f-7adf-47af-9960-9bcc938d4f5c" />
Successfully built a dual-VM SOC home lab consisting of a Windows endpoint and a Kali Linux attacker machine
<br>

<img width="1920" height="1080" alt="16-Reconfigured the Windows virtual machine to use an isolated Internal Network, preventing direct communication with the host or external internet" src="https://github.com/user-attachments/assets/feba7c82-9f1a-41b1-8dde-b88ddae1f77b" />
Reconfigured the Windows virtual machine to use an isolated Internal Network, preventing direct communication with the host or external internet

<br>

<img width="1920" height="1080" alt="17-Configured the Kali Linux VM to join the same isolated Internal Network for controlled communication with the Windows analysis workstation" src="https://github.com/user-attachments/assets/422a170f-4555-413b-a476-8e94bb049b3c" />
Configured the Kali Linux VM to join the same isolated Internal Network for controlled communication with the Windows analysis workstation

<br>

<img width="1920" height="1080" alt="19-Assigned a static IPv4 address to the Windows VM to enable predictables communication within the isolated lab network" src="https://github.com/user-attachments/assets/38fef270-1e05-4ad1-bf7c-747cbcd51cae" />
Assigned a static IPv4 address to the Windows VM to enable predictables communication within the isolated lab network
<br>

<img width="1920" height="1080" alt="21-Configured Kali Linux with a static IP address on the same subnet to support isolated host-to-host communication" src="https://github.com/user-attachments/assets/a7688bb3-10f4-48df-93f8-320af8d514de" />
Configured Kali Linux with a static IP address on the same subnet to support isolated host-to-host communication
<br>

<img width="1920" height="1080" alt="23-Verified successful communication between the Windows and Kal virtual machines across the isolated Internal Network while maintaining separation from the host operating system" src="https://github.com/user-attachments/assets/609b4314-a66d-44e6-af21-2885ddffd1cb" />
Verified successful communication between the Windows and Kal virtual machines across the isolated Internal Network while maintaining separation from the host operating system
<br>

<img width="1920" height="1080" alt="24-Splunk and Sysmon successfully configured  Verified telemetry ingestion by querying the endpoint index, confirming sysmon events are being collected and indexed for investigation" src="https://github.com/user-attachments/assets/19dc4512-5533-4881-a28e-963e58c721e2" />
Splunk and Sysmon successfully configured. Verified telemetry ingestion by querying the endpoint index, confirming sysmon events are being collected and indexed for investigation
<br>


### Phase 2 – Attack Simulation

<img width="1920" height="1080" alt="26-Confirmed Kali attacker VM IP addresss before generating lab traffic " src="https://github.com/user-attachments/assets/a8494b65-ab20-4862-863b-92f506874202" />
Confirmed Kali attacker VM IP addresss before generating lab traffic 
<br>

<img width="1920" height="1080" alt="27-Performed reconnaissance against the Windows endpoint and identified exposed services " src="https://github.com/user-attachments/assets/84e1d611-6dd0-4303-8ea5-83e042b2c75a" />
Performed reconnaissance against the Windows endpoint and identified exposed services 
<br>

<img width="1920" height="1080" alt="28-Created a controlled test executable using a double extension to generate endpoint telemetry" src="https://github.com/user-attachments/assets/67a39ccc-64de-4609-a10e-1ba6a04da599" />
Created a controlled test executable using a double extension to generate endpoint telemetry


<img width="1920" height="1080" alt="30-Hosted the test executable from Kali using a temporary Python HTTP server " src="https://github.com/user-attachments/assets/68e84e1f-ffee-49b8-b300-8522ccd26c64" />
Hosted the test executable from Kali using a temporary Python HTTP server 


<img width="1920" height="1080" alt="31-Enabled file extensions to reveal the true executable file type behind the double-extension filename" src="https://github.com/user-attachments/assets/45890a28-43fb-4eb1-bff7-0130175402bd" />
Enabled file extensions to reveal the true executable file type behind the double-extension filename


<img width="1920" height="1080" alt="32-Started a listener to receive the controlled reverse connection from the windows endpoint (UPDATED)" src="https://github.com/user-attachments/assets/cd87432c-6494-4a5e-9dc7-08ec36b90112" />
Started a listener to receive the controlled reverse connection from the windows endpoint (UPDATED)


<img width="1920" height="1080" alt="33-Successfully established a Meterpreter reverse TCP session from the Windows endpoint to the Kali attacker, confirming successful payload execution and remote access" src="https://github.com/user-attachments/assets/8ce2c24c-ae2d-45dc-8386-1ed55b05d202" />
Successfully established a Meterpreter reverse TCP session from the Windows endpoint to the Kali attacker, confirming successful payload execution and remote access


<img width="1920" height="1080" alt="34-Verified the Windows endpoint initiated a TCP connection to the Kali attacker&#39;s listener on port 4444 using netstat -anob " src="https://github.com/user-attachments/assets/4d953d93-938b-4724-9f1f-f284d110749a" />
Verified the Windows endpoint initiated a TCP connection to the Kali attacker's listener on port 4444 using netstat -anob 



### Phase 3 – Investigation

<img width="1920" height="1080" alt="35-Searched the Splunk endpoint index for Kali attacker IP (192 168 20 11) and identified Sysmon events associated with the malicious activity" src="https://github.com/user-attachments/assets/c65492d1-7dd7-4847-b50f-995c96701af3" />
Searched the Splunk endpoint index for Kali attacker IP (192.168.20.11) and identified Sysmon events associated with the malicious activity


<img width="1920" height="1080" alt="36-Examined the event fields and confirmed communication involving the Kali attacker IP (192 168 20 11), supporting the investigation of the unauthorized remote connection" src="https://github.com/user-attachments/assets/81054afe-46fe-4aa7-ab4f-79b225fad1b5" />
Examined the event fields and confirmed communication involving the Kali attacker IP (192.168.20.11), supporting the investigation of the unauthorized remote connection


<img width="1920" height="1080" alt="37-Identified Sysmon Process Creation (Event ID 1) events associated with the malicious executable Resume pdf exe, confirming that the malware execution was successfully ingested into Splunk" src="https://github.com/user-attachments/assets/ef0eaad3-57c9-41a6-a67c-36d5958f1d02" />
Identified Sysmon Process Creation (Event ID 1) events associated with the malicious executable Resume.pdf.exe, confirming that the malware execution was successfully ingested into Splunk


<img width="1920" height="1080" alt="38-Confirmed Resume pdf exe spawned cmd exe by correlating the ParentImage, ParentCommandLine, ParentProcessId, and ProcessGuid fields, establishing the parent-child process relationship" src="https://github.com/user-attachments/assets/aa6ac621-afd1-4b21-9105-2b60425af06f" />
Confirmed Resume.pdf.exe spawned cmd.exe by correlating the ParentImage, ParentCommandLine, ParentProcessId, and ProcessGuid fields, establishing the parent-child process relationship


<img width="1920" height="1080" alt="39-Pivoted on the Sysmon ProcessGuid to correlate related process creation events and reconstruct the execution chain associated with malicious process" src="https://github.com/user-attachments/assets/426eb585-20c0-4c54-a15c-5924d8f3e17f" />
Pivoted on the Sysmon ProcessGuid to correlate related process creation events and reconstruct the execution chain associated with malicious process


<img width="1920" height="1080" alt="40-Correlated events using the ProcessGuid and confirmed the malicious process executed host discovery commands including ipconfig, net user, and net localgroup" src="https://github.com/user-attachments/assets/971d16ff-ec28-4b83-bec0-a88de91a11b2" />
Correlated events using the ProcessGuid and confirmed the malicious process executed host discovery commands including ipconfig, net user, and net localgroup



## Indicators of Compromise (IOCs)

During the investigation, several Indicators of Compromise (IOCs) were identified that demonstrated successful execution of the simulated attack:

- Malicious executable (`Resume.pdf.exe`) executed on the Windows endpoint.
- Meterpreter reverse TCP session established between the victim and attacker.
- Suspicious process creation events recorded by Sysmon (Event ID 1).
- Network communication initiated from the compromised endpoint to the Kali Linux attacker.
- Parent-child process relationships indicating execution of the malicious payload.
- Process GUIDs used to correlate related events across the investigation.
- Splunk logs confirming endpoint telemetry associated with the simulated compromise.



## MITRE ATT&CK Mapping

| Tactic | Technique | Technique ID |
|---------|-----------|--------------|
| Initial Access | User Execution | T1204 |
| Execution | Command and Scripting Interpreter | T1059 |
| Execution | Malicious File Execution | T1204.002 |
| Command and Control | Application Layer Protocol | T1071 |
| Command and Control | Ingress Tool Transfer | T1105 |
| Discovery | System Information Discovery | T1082 |
| Discovery | Process Discovery | T1057 |
| Defense Evasion | Masquerading (Resume.pdf.exe) | T1036 |



## Key Findings

- Successfully built a fully functional SOC home lab capable of generating realistic attack telemetry.
- Verified that Sysmon captured detailed endpoint events throughout the simulated compromise.
- Confirmed that the Splunk Universal Forwarder successfully transmitted endpoint telemetry to Splunk Enterprise.
- Reconstructed the complete attack timeline by correlating process creation events and network activity.
- Identified malicious process execution, command-and-control communication, and related endpoint artifacts.
- Demonstrated the effectiveness of centralized log collection for endpoint investigations.
- Validated that Splunk can rapidly identify suspicious endpoint behavior using Sysmon telemetry.



## Lessons Learned

This project reinforced the importance of high-quality endpoint telemetry for incident investigations. Building the lab from scratch provided practical experience configuring a SIEM, deploying endpoint logging, and troubleshooting data ingestion issues. Simulating a controlled compromise demonstrated how attacker actions translate into Windows telemetry and how those events can be correlated within Splunk to reconstruct an attack timeline.

Beyond the technical implementation, this project strengthened my understanding of SOC investigation workflows, log analysis, endpoint visibility, and the importance of documenting findings in a clear and repeatable manner. These skills provide a strong foundation for performing real-world Security Operations Center investigations.
