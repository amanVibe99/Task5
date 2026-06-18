# SentinelAuth: Mini-SIEM Deployment & Incident Response Lab

## 📌 Project Overview
SentinelAuth is a localized, high-performance Security Information and Event Management (SIEM) pipeline designed to ingest, parse, and analyze real-time Linux authentication telemetry. This project demonstrates a full-loop incident response scenario—moving from baseline monitoring to active brute-force threat detection and automated firewall containment.

## 🏗️ Technical Architecture
The deployment architecture utilizes a three-tier localized virtual network matrix:
* **Log Ingestion & Mitigation Engine:** Ubuntu Server hosting optimized microservice containers.
* **Adversary Emulation Platform:** Kali Linux VM simulating multi-threaded credential-stuffing network attacks.
* **Analyst Dashboard View:** Managed via a bridged network interface on the host machine web browser.

### 🔄 Telemetry Data Flow Pipeline
Every operating system event moves through a structured pipeline before rendering on the security control interface:

`Ubuntu Auth Logs (/var/log/auth.log) ──> Filebeat Agent ──> Elasticsearch DB (Port 9200) ──> Kibana Interface (Port 5601)`

---

## 📊 Incident Response Timeline & NIST Framework Analysis

| Timestamp (IST) | Incident Phase | Event Details / Defensive Actions Taken |
| :--- | :--- | :--- |
| **10:35 AM** | **Preparation & Baseline** | Initialized Filebeat system monitoring modules. Standard baseline infrastructure authentication logs began streaming smoothly into the centralized database. |
| **10:47 AM** | **Attack Simulation** | Launched a high-velocity SSH brute-force credential attack from the Kali Linux adversary platform utilizing `Hydra`. |
| **10:48 AM** | **Incident Detection** | Identified an aggressive anomaly spike (**48 authentication failures**) within the Kibana Discover dashboard using target KQL filtering (`event.outcome : "failure"`). Isolated critical Indicators of Compromise (IoCs), including target administrative usernames and the adversary's network address (`192.168.0.102`). |
| **10:52 AM** | **Containment & Eradication** | Enforced immediate network isolation by activating the host packet-filtering layer (`UFW`) and applying a strict traffic drop rule to block all further communication from the malicious IP address. |
| **10:55 AM** | **Post-Incident Review** | Validated successful remediation. Threat actor sessions were fully terminated, and incoming malicious authentication logs dropped permanently back to zero. |

---

## 📸 Technical Artifacts & Evidence

### 1. Microservices Architecture Deployment
Open-source configuration blueprint detailing the containerized Elasticsearch and Kibana environment:
![Docker Setup](assets/01_docker_setup.png)

### 2. SIEM Core Engine Verification
Centralized monitoring console loading successfully across the internal host network bridge:
![SIEM Dashboard](assets/02_siem_dashboard.png)

### 3. Brute-Force Anomaly Detection
The specific KQL query capturing the exact signature of the live 48-hit brute-force attack:
![Attack Detection](assets/03_attack_detection.png)

### 4. Firewall Containment Execution
Active packet filter status verifying the permanent drop rule applied against the threat actor:
![Containment Firewall](assets/04_containment_firewall.png)

---
*Developed as part of the Technical Capstone Project portfolio requirement.*