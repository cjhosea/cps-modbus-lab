
# CPS Modbus Lab

This lab is an example of the type of incidents that can occur in an ICS/OT environment. Critical infrastructure, such as those found in water plants and electrical grids, are vital to the safety and well-being of our modern societies.


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

## Purdue Model
![](https://github.com/cjhosea/cps-modbus-lab/blob/main/media/Modbus%20Lab%20Purdue%20Model.png)
## Network Diagram
![](https://github.com/cjhosea/cps-modbus-lab/blob/main/media/Modbus%20Lab%20Network%20Diagram.png)

## OT Incident Triage Report
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



## Modbus Lab Incident Report
![](https://github.com/cjhosea/cps-modbus-lab/blob/main/media/ModbusReplayAttackLog.jpg)

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



![](https://github.com/cjhosea/cps-modbus-lab/blob/main/media/capture_led_on_pcap.png)



