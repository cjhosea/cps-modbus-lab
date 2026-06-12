
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
![]([https://github.com/cjhosea/](https://github.com/cjhosea/cps-modbus-lab/blob/main/media/OT%20Incident%20Triage%20Report.pdf))

## Modbus Lab Incident Report
![](https://github.com/cjhosea/cps-modbus-lab/blob/main/media/ModbusReplayAttackLog.jpg)
**OT Incident Triage Report**

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


![](https://github.com/cjhosea/cps-modbus-lab/blob/main/media/capture_led_on_pcap.png)



