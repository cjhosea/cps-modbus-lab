
# CPS Modbus Lab

This lab is an example of the type of incidents that can occur in an ICS/OT environment. Critical infrastructure, such as those found in water plants and electrical grids, are vital to the safety and well-being of our modern societies. The most important things in any OT environment are availability and safety, and any disruption can cause catastrophic effects to those in or around the site, as well as the environment. 


## Repository Layout
```text
cps-modbus-lab/
├── server/            # Modbus server
├── attack/            # Scapy attack scripts (attacker)
├── defense/
│   ├── scripts/       # IDS 
│   └── logs/          # alerts
├── docs/              # write‑ups
├── README.md          # this file
```
## MITRE ATT&CK Mapping
| Attack Technique         | ID    |
| ------------------------ | ----- |
| Unauthorized Message: Command Message  | T1692.001  |

T1692.001 of the MITRE ATT&CK for ICS framework represents "Unauthorized Message: Command Message." This is a sub-technique of T1692 (Unauthorized Message). Using this technique, adversaries are able to send unauthorized commands to control systems to perform actions that are not in their expected functionality. This technique can be associated with the following tactics: Evasion and Impair Process Control. In this lab, the tactic demonstrated would fall under Impair Process Control, which is when the threat actor is trying to "manipulate, disable, or damage physical control processes." Two prominent examples of this technique are the 2015 Ukraine Electric Power Attacks, in which the Sandworm Team sent unauthorized commands to substation devices and left citizens of Ukraine without power for many hours, and the TRISIS attack in 2017, where the attacker group TEMP.Veles used Triton malware to send unauthorized commands to safety controllers.  

## Purdue Model
![](https://github.com/cjhosea/cps-modbus-lab/blob/main/media/Modbus%20Lab%20Purdue%20Model.png)
## Network Diagram
![](https://github.com/cjhosea/cps-modbus-lab/blob/main/media/Modbus%20Lab%20Network%20Diagram.png)

## OT Incident Triage Report
![](https://github.com/cjhosea/cps-modbus-lab/blob/main/media/ModbusReplayAttackLog.jpg)
![](https://github.com/cjhosea/cps-modbus-lab/blob/main/media/capture_led_on_pcap.png)
| Alert | Modbus Replay Attack |
| :---- | :---- |
| **Source** | 192.168.86.46 |
| **Destination** | 192.168.86.49 |
| **Protocol** | Modbus TCP (port 502\) |
| **Function Code** | 05 (Write Single Coil) |
| **Suspected Behavior** | Unauthorized Message: Command Message (T1692.001)  |
| **Potential Operational Impact** | Poses a risk to public health due to unsafe water |
| **Recommended Response** | Ask the operator or engineer to verify the state of the affected device. Once deemed safe to do, block traffic from source to destination, while preserving PCAPs and investigating source device. |
| **Escalation Path** | OT Analyst \-\> Senior OT Analyst \-\> OT Security Manager \-\> Control Systems Engineer \-\> CISO / Plant Manager |

Modbus is the most widely used fieldbus protocol. It allows field devices to communicate with controllers and works via a request/reponse communication method. The function code decides what action the slave/outstation should take. Function code 05 (write single coil), in this case, writes a single bit to the output (coil). This is essentially just a singular ON or OFF switch. In an OT environment, this could represent the shutting or opening of a valve or pump. 


## Modbus Lab Incident Report

**What Happened and When?**

| When did the incident occur? | 06/16/2025, 09:53:56 \- 09:59:16 AM |
| :---- | :---- |
| What was the nature of the incident? | Malicious commands sent to PLC. |
| Which specific assets were at risk? | HMI (A0002), Control Server (A0007), PLC (A0003) and corresponding field devices |
| What is the severity or significance of the incident? | Threat actor could cause physical damage to plant and/or faculty. |

**What was the Root Cause?**

| What caused the incident? | Attacker likely exploited a vulnerability in HMI.  |
| :---- | :---- |
| How do we know? | Analysis of Suricata logs show attacker was able to send unauthorized messages to PLC (T1692.001).  |

**What Was and Remains to Be Done?**

| Identification: How was the problem detected? | Attack was detected via Suricata IDS.  |
| :---- | :---- |
| Containment: How will we be able to limit the incident’s scope, including adverse effects on the affected data and systems? | Isolate the HMI and PLC. |
| Eradication: What steps need to be taken to eliminate adversarial presence from the affected environment, protect the affected data, or minimize the risks to the affected parties? | Reset all passwords in the environment and verify all ACL and firewall configurations. If necessary (e.g. rootkit), rebuild with new hardware. |
| Recovery: How can we restore normal business operations or normal activities? | Ensure safety and control systems are operating as expected. When ready, bring interdependent systems back up properly.  |





