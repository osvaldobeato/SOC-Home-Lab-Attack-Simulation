# Images

This folder contains the screenshots used throughout the project documentation.

<br>

<img width="1920" height="1080" alt="1-Starting with a clean Windows host before building the SOC home lab" src="https://github.com/user-attachments/assets/1ea6e69b-0f59-4177-aa12-dc8e33f5afe7" />


<img width="1920" height="1080" alt="2-Downloading Oracle VirtualBox to create the virtual lab Environment" src="https://github.com/user-attachments/assets/4898a705-cd05-42d0-aa8f-9d78f525f6e6" />


<img width="1920" height="1080" alt="3-Verified the VirtualBox installer intergrity using SHA256 before installation  This is a great screenshot because it shows security awareness" src="https://github.com/user-attachments/assets/a7f8d225-5df9-4ca5-9e96-5a89434d2ec6" />


<img width="1920" height="1080" alt="5-VirtualBox successfully installed and ready to host virtual machines " src="https://github.com/user-attachments/assets/dd7af653-f346-4de0-b785-6a2e53383c44" />


<img width="1920" height="1080" alt="7-Creating te Windows 10 virtual machine and allocating system resources " src="https://github.com/user-attachments/assets/2e70501f-692b-4c1b-9bd9-bfe481d65f95" />


<img width="1920" height="1080" alt="11-Windows 10 virtual machine successfully deployed" src="https://github.com/user-attachments/assets/7e97d230-0ea4-4509-96a7-2cfeeb0036c4" />


<img width="1920" height="1080" alt="13-Successfully built a dual-VM SOC home lab consisting of a Windows endpoint and a Kali Linux attacker machine " src="https://github.com/user-attachments/assets/9f3a547b-4d2b-49c2-840e-b5e7835837bd" />


<img width="1920" height="1080" alt="16-Reconfigured the Windows virtual machine to use an isolated Internal Network, preventing direct communication with the host or external internet" src="https://github.com/user-attachments/assets/7baf2935-73c0-463c-a54a-68daa9202e48" />


<img width="1920" height="1080" alt="17-Configured the Kali Linux VM to join the same isolated Internal Network for controlled communication with the Windows analysis workstation" src="https://github.com/user-attachments/assets/97e77995-811c-4e7b-8391-4868f9d51c90" />


<img width="1920" height="1080" alt="19-Assigned a static IPv4 address to the Windows VM to enable predictables communication within the isolated lab network" src="https://github.com/user-attachments/assets/9ec5ba1f-4cd6-4205-8947-055a25fc3a80" />


<img width="1920" height="1080" alt="21-Configured Kali Linux with a static IP address on the same subnet to support isolated host-to-host communication" src="https://github.com/user-attachments/assets/d6e9f566-7cf1-4c03-8e6f-4821e884dac9" />


<img width="1920" height="1080" alt="23-Verified successful communication between the Windows and Kal virtual machines across the isolated Internal Network while maintaining separation from the host operating system" src="https://github.com/user-attachments/assets/61d9d4d9-6d58-4158-afa8-47660872b686" />


<img width="1920" height="1080" alt="24-Splunk and Sysmon successfully configured  Verified telemetry ingestion by querying the endpoint index, confirming sysmon events are being collected and indexed for investigation" src="https://github.com/user-attachments/assets/a15151f5-2bab-4f7b-bcd7-2e80e25b33ef" />


<img width="1920" height="1080" alt="26-Confirmed Kali attacker VM IP addresss before generating lab traffic " src="https://github.com/user-attachments/assets/ff06085c-097e-432e-aaf7-5feca7c86c92" />


<img width="1920" height="1080" alt="27-Performed reconnaissance against the Windows endpoint and identified exposed services " src="https://github.com/user-attachments/assets/cd921406-7119-4676-bbd8-8cdc65ee8389" />


<img width="1920" height="1080" alt="28-Created a controlled test executable using a double extension to generate endpoint telemetry" src="https://github.com/user-attachments/assets/18cfcabf-0070-4055-84f0-6927365cf845" />


<img width="1920" height="1080" alt="29-Started a listener to receive the controlled reverse connection from the windows endpoint" src="https://github.com/user-attachments/assets/4a8477b5-9e25-4315-8562-766dc24f44b5" />


<img width="1920" height="1080" alt="30-Hosted the test executable from Kali using a temporary Python HTTP server " src="https://github.com/user-attachments/assets/e5a80456-d59d-4668-bc61-d9a4ff02b29a" />


<img width="1920" height="1080" alt="31-Enabled file extensions to reveal the true executable file type behind the double-extension filename" src="https://github.com/user-attachments/assets/b57c6b82-5eb3-4092-8d55-0a997e572f71" />


<img width="1920" height="1080" alt="32-Started a listener to receive the controlled reverse connection from the windows endpoint (UPDATED)" src="https://github.com/user-attachments/assets/cffc5b9d-c8a8-438f-a435-aa321979b1dd" />


<img width="1920" height="1080" alt="33-Successfully established a Meterpreter reverse TCP session from the Windows endpoint to the Kali attacker, confirming successful payload execution and remote access" src="https://github.com/user-attachments/assets/8e3808ed-3b5d-4a40-b45c-f13c655aa84b" />


<img width="1920" height="1080" alt="34-Verified the Windows endpoint initiated a TCP connection to the Kali attacker&#39;s listener on port 4444 using netstat -anob " src="https://github.com/user-attachments/assets/0ecc91d2-253c-4de0-bd0d-f3db70c1d5ff" />


<img width="1920" height="1080" alt="35-Searched the Splunk endpoint index for Kali attacker IP (192 168 20 11) and identified Sysmon events associated with the malicious activity" src="https://github.com/user-attachments/assets/d6309acf-7611-4cae-a9e2-424866dee30b" />


<img width="1920" height="1080" alt="36-Examined the event fields and confirmed communication involving the Kali attacker IP (192 168 20 11), supporting the investigation of the unauthorized remote connection" src="https://github.com/user-attachments/assets/a848d2d0-4d7b-4a12-9be4-37a885599959" />


<img width="1920" height="1080" alt="37-Identified Sysmon Process Creation (Event ID 1) events associated with the malicious executable Resume pdf exe, confirming that the malware execution was successfully ingested into Splunk" src="https://github.com/user-attachments/assets/0b7ab486-f8d8-4bdf-9d13-1bcec48513a2" />


<img width="1920" height="1080" alt="38-Confirmed Resume pdf exe spawned cmd exe by correlating the ParentImage, ParentCommandLine, ParentProcessId, and ProcessGuid fields, establishing the parent-child process relationship" src="https://github.com/user-attachments/assets/078c26f9-43ea-4491-8d79-331646b0c6e4" />


<img width="1920" height="1080" alt="39-Pivoted on the Sysmon ProcessGuid to correlate related process creation events and reconstruct the execution chain associated with malicious process" src="https://github.com/user-attachments/assets/59c08559-62d0-44e5-8da8-b4ae80b2db29" />


<img width="1920" height="1080" alt="40-Correlated events using the ProcessGuid and confirmed the malicious process executed host discovery commands including ipconfig, net user, and net localgroup" src="https://github.com/user-attachments/assets/d65f0502-5df2-4181-bf58-1e78c9a8489a" />


<img width="1383" height="834" alt="41- Diagram" src="https://github.com/user-attachments/assets/10a89217-eee2-4159-b3da-940d3c72be41" />
