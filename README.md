# Splunk SIEM Home Lab — Log Ingestion & Monitoring

A home lab built to get hands-on experience with Splunk as a SIEM platform. The focus of this lab was setting up log ingestion pipelines from multiple sources and learning how to navigate and query logs inside the Splunk interface.

---

## Lab Architecture

| Machine | OS | Role |
|---|---|---|
| Splunk Server | Ubuntu | Splunk manager + dashboard |
| Apache Server | Ubuntu | Web server generating access logs |
| FortiGate | FortiGate VM | Firewall generating network/traffic logs |

All machines run as virtual machines on the same host.

---

## What This Lab Covers

- Deploying and configuring a Splunk instance on Ubuntu from scratch
- Configuring an Apache web server to generate access logs
- Setting up a FortiGate firewall VM to generate network traffic logs
- Forwarding logs from both sources into the Splunk server
- Using the Splunk Search & Reporting interface to query and explore logs across both sources

---

## How the Log Pipeline Works
Apache Server (Ubuntu)          FortiGate VM
|                             |
Access logs generated        Firewall/traffic logs generated
|                             |
└──────────┬──────────────────┘
↓
Splunk Server (Ubuntu)
↓
Logs indexed and searchable
via Splunk Web interface

---

## Key Configuration

**1. Forwarding Apache logs to Splunk**

Configured the Splunk Universal Forwarder on the Apache VM to monitor and ship the Apache access log:
[monitor:///var/log/apache2/access.log]
index = main
sourcetype = access_combined

**2. Forwarding FortiGate logs to Splunk**

Configured FortiGate to send syslog to the Splunk server's IP on UDP port 514. On the Splunk server, set up a UDP data input to receive and index the incoming syslog:
Settings → Data Inputs → UDP → Port 514
Sourcetype: syslog
Index: main

---

## Screenshots

<img width="1919" height="1063" alt="image" src="https://github.com/user-attachments/assets/ac350532-c066-4304-bd6c-f87fe7ba55d6" />
<img width="1870" height="943" alt="image" src="https://github.com/user-attachments/assets/47fa2040-3de2-4f63-94f3-0a597d966d38" />
<img width="1861" height="940" alt="image" src="https://github.com/user-attachments/assets/f944b2b6-7bd9-438e-81b7-1f1eac859a83" />
<img width="1863" height="939" alt="image" src="https://github.com/user-attachments/assets/a92fcdf5-9b25-47fb-842a-76cec778f7d3" />


---

## Tools & Technologies

- **Splunk** — SIEM platform (search, indexing, dashboards)
- **Apache HTTP Server** — web server log source
- **FortiGate** — firewall log source
- **Splunk Universal Forwarder** — log shipping agent
- **VirtualBox / VMware** — virtualisation
- **Ubuntu** — server operating system

---

## What I Learned

- How a SIEM ingests and indexes logs from different source types
- The difference between agent-based log forwarding (Universal Forwarder) and syslog-based ingestion
- How to use Splunk's Search Processing Language (SPL) to query and filter logs
- How network and web server logs complement each other for security monitoring

---

## References

- [Splunk Documentation — Universal Forwarder](https://docs.splunk.com/Documentation/Forwarder)
- [Splunk Documentation — Getting Data In](https://docs.splunk.com/Documentation/Splunk/latest/Data/WhatSplunkcanmonitor)
- [FortiGate — Configuring Syslog](https://docs.fortinet.com/document/fortigate/7.4.0/administration-guide/696010/configuring-syslog)
- [Splunk Basics Course — Udemy](https://www.udemy.com/course/splunk-basics-course/learn/lecture/20456607#overview)
