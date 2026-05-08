# Architecture — Home SOC Mini Lab

## Objective

Home SOC Mini Lab is a small cybersecurity lab designed to practice basic Blue Team and SOC workflows in a controlled virtual environment.

The objective of this architecture is to explain how the lab will collect logs, centralize security events, detect suspicious activity, and support a basic incident investigation.

The first version of the lab focuses on one realistic detection scenario: failed SSH login attempts on a Linux endpoint.

This architecture is intentionally minimal. The goal is not to build a production-grade SOC, but to create a clear and documented MVP that can be presented on GitHub, in a CV, and during interviews.

---

## Architecture Overview

The lab follows a simple endpoint-to-server monitoring model.

A Linux endpoint generates system and authentication logs. A Wazuh Agent installed on the endpoint collects those logs and forwards security events to the Wazuh Server. The Wazuh Server analyzes the events and displays alerts in the Wazuh Dashboard, where the analyst can review and document the incident.

Architecture flow:

Ubuntu Server / Linux Endpoint  
→ Wazuh Agent  
→ Wazuh Server  
→ Wazuh Dashboard  
→ Incident Investigation

The main workflow is:

1. The Linux endpoint generates system and authentication logs.
2. The Wazuh Agent collects relevant logs from the endpoint.
3. The logs are forwarded to the Wazuh Server.
4. The Wazuh Server analyzes the events.
5. Alerts are displayed in the Wazuh Dashboard.
6. The analyst reviews the alert and writes an incident report.

---

## Components

### Wazuh Server

The Wazuh Server is the central security monitoring component of the lab.

Its role is to receive events from monitored endpoints, analyze them with security rules, and generate alerts when suspicious activity is detected.

In this project, Wazuh acts as the main SIEM-like platform.

Main responsibilities:

- receive security events from the Linux endpoint;
- analyze Linux system and authentication logs;
- generate alerts based on suspicious activity;
- provide a dashboard for investigation;
- centralize security visibility for the lab.

### Ubuntu Server

The Ubuntu Server is the main Linux machine used in the lab.

It represents a basic server that could exist in a real company environment. In this MVP, it will be used to generate system logs and authentication logs, especially SSH-related logs.

Main responsibilities:

- act as the monitored Linux server;
- run the SSH service;
- generate authentication logs;
- provide local logs for the Wazuh Agent.

Important log files:

- `/var/log/auth.log`
- `/var/log/syslog`

### Linux Endpoint

The Linux Endpoint is the monitored host where the Wazuh Agent is installed.

For the first version of the lab, the Ubuntu Server and the Linux Endpoint can be the same virtual machine.

Main responsibilities:

- run the Wazuh Agent;
- collect local Linux logs;
- forward events to the Wazuh Server;
- generate test activity for detection scenarios.

In a real SOC environment, endpoints are important because they generate many of the security events that analysts investigate.

---

## Data Flow

The data flow starts from the Linux endpoint and ends with the investigation in the Wazuh Dashboard.

When someone tries to connect to the Ubuntu Server through SSH with incorrect credentials, the failed login event is written into the Linux authentication log.

The Wazuh Agent reads this log and forwards the event to the Wazuh Server. The Wazuh Server analyzes the event using detection rules. If the activity matches a suspicious pattern, an alert is created and displayed in the dashboard.

Simplified data flow:

Failed SSH login attempt  
→ Linux authentication log  
→ Wazuh Agent  
→ Wazuh Server  
→ Wazuh Dashboard  
→ Incident investigation

This represents a basic SOC workflow:

Collect logs  
→ Detect suspicious activity  
→ Investigate alert  
→ Document findings

---

## Network Assumption

The lab will run in a local virtualized environment.

Planned setup:

- VM 1: Wazuh Server
- VM 2: Ubuntu Server / Linux Endpoint

Both virtual machines should be connected to the same virtual network so that the Wazuh Agent can communicate with the Wazuh Server.

Network assumptions:

- the lab runs on a local host machine;
- VirtualBox or VMware is used for virtualization;
- the Wazuh Server and Ubuntu Endpoint are on the same virtual network;
- the Ubuntu Endpoint can reach the Wazuh Server using its private IP address;
- SSH is enabled on the Ubuntu Endpoint;
- internet access may be required during installation;
- the lab is isolated from production systems.

The exact IP addresses will be documented later during the setup phase.

Temporary placeholders:

- Wazuh Server IP: to be defined
- Ubuntu Endpoint IP: to be defined

---

## Detection Scenario

The first detection scenario is failed SSH login attempts.

This scenario was chosen because it is simple, realistic, and directly related to SOC monitoring.

In a real environment, repeated failed SSH login attempts may indicate:

- password guessing;
- brute-force attempts;
- unauthorized access attempts;
- reconnaissance against an exposed SSH service.

In this lab, the scenario will be simulated in a controlled environment by trying to connect to the Ubuntu Endpoint through SSH using incorrect credentials.

Expected behavior:

1. SSH login attempts fail on the Ubuntu Endpoint.
2. The failed attempts are written to `/var/log/auth.log`.
3. The Wazuh Agent collects the authentication events.
4. The Wazuh Server analyzes the events.
5. Wazuh generates authentication-related alerts.
6. The analyst reviews the alert in the dashboard.

Expected information to review:

- source IP address;
- targeted username;
- timestamp;
- number of failed attempts;
- event description;
- alert severity;
- related Wazuh rule.

Example incident classification:

- Type: Authentication attack
- Category: Failed SSH login attempts
- Severity: Low to Medium in lab context
- Status: Investigated

Key investigation questions:

- Which IP address generated the failed login attempts?
- Which account was targeted?
- How many attempts were made?
- When did the attempts happen?
- Does the activity look accidental or suspicious?
- What would be the recommended response in a real company environment?

---

## Current Limitations

This architecture is the first MVP version of the lab, so it has several limitations.

Current limitations:

- only one Linux endpoint is included;
- only one detection scenario is planned;
- Windows event logs are not included yet;
- custom Wazuh rules are not included yet;
- automated blocking or response is not configured;
- no advanced threat hunting is included;
- no production hardening is applied;
- screenshots and incident reports are not completed yet.

These limitations are acceptable for v0 because the priority is to build a clean and understandable SOC workflow before adding complexity.

The main objective of this version is to show that the lab can collect logs, detect suspicious activity, and support a basic investigation.

---

## Next Improvements

The next step is to move from documentation to implementation.

Planned improvements:

1. Install the Wazuh Server.
2. Create the Ubuntu Endpoint virtual machine.
3. Install the Wazuh Agent on the endpoint.
4. Connect the agent to the Wazuh Server.
5. Verify that the endpoint appears in the Wazuh Dashboard.
6. Enable SSH on the Ubuntu Endpoint.
7. Generate failed SSH login attempts.
8. Review alerts in Wazuh.
9. Take screenshots as proof.
10. Write the first incident report.

Planned documentation files:

- `docs/setup.md`
- `docs/commands.md`
- `docs/incidents/incident-001-failed-ssh-login.md`

Future improvements:

- add Kali Linux as a controlled attacker machine;
- add Nmap scan detection;
- add Windows endpoint monitoring;
- create custom Wazuh detection rules;
- document false positive analysis;
- add more incident reports;
- improve the architecture diagram later;
- add troubleshooting notes.

---

## Version Status

Architecture version: v0  
Project phase: Documentation and architecture preparation  
Main tool: Wazuh  
Endpoint: Ubuntu Server / Linux Endpoint  
First detection scenario: Failed SSH login attempts  
Next milestone: Install Wazuh Server and connect the first endpoint