# Home SOC Mini Lab — Log Monitoring & Incident Detection Environment

> This README contains two versions in the same file:
>
> 1. English version
> 2. French version below
>
> Ce README contient deux versions dans le même fichier :
>
> 1. Version anglaise
> 2. Version française ci-dessous

---

# English Version

## 1. Project Overview

**Home SOC Mini Lab** is a small cybersecurity lab designed to collect, monitor, and investigate security logs from Linux endpoints using open-source security tools.

The objective of this project is to build a presentable Blue Team / SOC-oriented portfolio project for GitHub, CV, and interviews.

The lab focuses on core SOC fundamentals:

- Log collection
- Security monitoring
- Alert detection
- Basic incident investigation
- Technical documentation

This MVP does not aim to build an overcomplicated enterprise-grade SOC environment. Instead, it focuses on one clear detection scenario, a clean architecture, screenshots, setup steps, and a basic incident report.

---

## 2. Project Goal

The goal of this project is to create a small virtual SOC lab capable of:

- Collecting Linux authentication logs
- Monitoring endpoint activity
- Detecting suspicious SSH login activity
- Investigating alerts in Wazuh
- Documenting the full workflow for GitHub and interviews

This project is mainly focused on Blue Team fundamentals and entry-level SOC Analyst skills.

---

## 3. Lab Architecture

The initial architecture is based on two virtual machines.

### VM 1 — Wazuh Server

Purpose:

- Collect logs from endpoints
- Analyze security events
- Generate alerts
- Provide a dashboard for investigation

### VM 2 — Ubuntu Endpoint

Purpose:

- Act as a Linux endpoint
- Generate authentication logs
- Send logs to the Wazuh Server through the Wazuh Agent

---

## 4. Planned Tools

Core tools used in the MVP:

- Ubuntu host machine
- VirtualBox
- Ubuntu Server VM
- Ubuntu Endpoint VM
- Wazuh Server
- Wazuh Agent
- Linux system logs
- SSH service
- GitHub documentation

Possible future tools:

- Kali Linux VM for attack simulation
- Wireshark for network observation
- Python for simple log parsing
- Windows VM with Sysmon
- Splunk Free for SIEM comparison

---

## 5. Logs Collected

The first version of the lab focuses on Linux system and authentication logs.

Initial logs:

```txt
/var/log/auth.log
/var/log/syslog
```

Main focus:

- SSH authentication logs
- Failed login attempts
- Successful login events
- Sudo-related events
- Basic system activity logs

---

## 6. First Detection Scenario

### Scenario Chosen

```txt
Failed SSH login attempts / suspicious login logs
```

### Scenario Description

An Ubuntu endpoint receives multiple failed SSH login attempts.

The Linux system records these attempts in:

```txt
/var/log/auth.log
```

The Wazuh Agent installed on the endpoint collects these logs and sends them to the Wazuh Server.

Wazuh analyzes the logs and generates alerts related to authentication failures.

---

## 7. Expected Investigation Workflow

The expected workflow is:

1. Generate failed SSH login attempts against the Ubuntu endpoint
2. Confirm failed login traces inside `/var/log/auth.log`
3. Check the Wazuh dashboard for related alerts
4. Capture screenshots of the detection
5. Write a short incident report
6. Document what happened, what was detected, and what could be improved

---

## 8. Expected GitHub Repository Structure

```txt
home-soc-mini-lab/
├── README.md
├── docs/
│   ├── architecture.md
│   ├── setup-wazuh.md
│   ├── setup-agent-linux.md
│   └── detection-scenarios.md
├── diagrams/
│   └── architecture.png
├── reports/
│   └── incident-report-001-ssh-bruteforce.md
├── screenshots/
│   ├── wazuh-dashboard.png
│   ├── agent-active.png
│   ├── ssh-failed-login-alert.png
│   └── investigation-view.png
└── scripts/
    └── parse_auth_log.py
```

---

## 9. Expected Final Output

By the end of the MVP, the project should include:

- A functional Wazuh Server
- One monitored Ubuntu endpoint
- SSH authentication logs collected by Wazuh
- At least one detection scenario
- Screenshots of the dashboard and alerts
- A short incident report
- Clear setup documentation
- A GitHub-ready project structure

---

## 10. CV Description

**Home SOC Mini Lab — Log Monitoring & Incident Detection Environment**

Built a virtual SOC lab using Wazuh and Linux endpoints to collect authentication logs, detect failed SSH login attempts, and document a basic incident investigation workflow with screenshots, setup steps, and an incident report.

---

## 11. Project Status

```txt
MVP scope written: yes
Tools chosen: Ubuntu, VirtualBox, Wazuh, Ubuntu Endpoint, SSH, Linux logs
First detection scenario: Failed SSH login attempts
Repository name idea: home-soc-mini-lab
Main blocker: Lab installation and practical setup still need to be completed
```

---

# Version Française

## 1. Présentation du projet

**Home SOC Mini Lab** est un petit laboratoire de cybersécurité conçu pour collecter, superviser et analyser des journaux de sécurité provenant d’endpoints Linux à l’aide d’outils open-source.

L’objectif de ce projet est de construire un projet orienté Blue Team / SOC, présentable sur GitHub, dans un CV et lors d’entretiens.

Le lab se concentre sur les fondamentaux SOC suivants :

- Collecte de logs
- Supervision de sécurité
- Détection d’alertes
- Investigation d’incident basique
- Documentation technique

Ce MVP n’a pas pour objectif de construire un SOC complexe de niveau entreprise. Il se concentre plutôt sur un scénario de détection clair, une architecture simple, des captures d’écran, des étapes d’installation et un rapport d’incident basique.

---

## 2. Objectif du projet

L’objectif de ce projet est de créer un petit lab SOC virtualisé capable de :

- Collecter des journaux d’authentification Linux
- Superviser l’activité d’un endpoint
- Détecter une activité SSH suspecte
- Investiguer des alertes dans Wazuh
- Documenter le workflow complet pour GitHub et les entretiens

Ce projet est principalement orienté vers les fondamentaux Blue Team et les compétences d’un SOC Analyst junior.

---

## 3. Architecture du lab

L’architecture initiale repose sur deux machines virtuelles.

### VM 1 — Wazuh Server

Rôle :

- Collecter les logs des endpoints
- Analyser les événements de sécurité
- Générer des alertes
- Fournir un dashboard pour l’investigation

### VM 2 — Ubuntu Endpoint

Rôle :

- Représenter une machine Linux supervisée
- Générer des journaux d’authentification
- Envoyer les logs au Wazuh Server via le Wazuh Agent

---

## 4. Outils prévus

Outils principaux utilisés dans le MVP :

- Machine hôte Ubuntu
- VirtualBox
- VM Ubuntu Server
- VM Ubuntu Endpoint
- Wazuh Server
- Wazuh Agent
- Journaux système Linux
- Service SSH
- Documentation GitHub

Outils possibles pour une future extension :

- VM Kali Linux pour simuler des attaques
- Wireshark pour l’observation réseau
- Python pour parser simplement des logs
- VM Windows avec Sysmon
- Splunk Free pour comparaison avec un autre SIEM

---

## 5. Logs collectés

La première version du lab se concentre sur les journaux système et les journaux d’authentification Linux.

Logs initiaux :

```txt
/var/log/auth.log
/var/log/syslog
```

Focus principal :

- Logs d’authentification SSH
- Tentatives de connexion échouées
- Connexions réussies
- Événements liés à sudo et à l’authentification
- Activité système basique

---

## 6. Premier scénario de détection

### Scénario choisi

```txt
Tentatives de connexion SSH échouées / logs de connexion suspects
```

### Description du scénario

Un endpoint Ubuntu reçoit plusieurs tentatives de connexion SSH échouées.

Le système Linux enregistre ces tentatives dans :

```txt
/var/log/auth.log
```

L’agent Wazuh installé sur l’endpoint collecte ces logs et les envoie au Wazuh Server.

Wazuh analyse les logs et génère des alertes liées aux échecs d’authentification.

---

## 7. Workflow d’investigation attendu

Le workflow attendu est le suivant :

1. Générer des tentatives de connexion SSH échouées contre l’endpoint Ubuntu
2. Vérifier les traces dans `/var/log/auth.log`
3. Consulter le dashboard Wazuh pour trouver les alertes liées
4. Capturer des screenshots de la détection
5. Rédiger un court rapport d’incident
6. Documenter ce qui s’est passé, ce qui a été détecté et ce qui pourrait être amélioré

---

## 8. Structure GitHub prévue

```txt
home-soc-mini-lab/
├── README.md
├── docs/
│   ├── architecture.md
│   ├── setup-wazuh.md
│   ├── setup-agent-linux.md
│   └── detection-scenarios.md
├── diagrams/
│   └── architecture.png
├── reports/
│   └── incident-report-001-ssh-bruteforce.md
├── screenshots/
│   ├── wazuh-dashboard.png
│   ├── agent-active.png
│   ├── ssh-failed-login-alert.png
│   └── investigation-view.png
└── scripts/
    └── parse_auth_log.py
```

---

## 9. Résultat final attendu

À la fin du MVP, le projet devrait contenir :

- Un Wazuh Server fonctionnel
- Un endpoint Ubuntu supervisé
- Des logs SSH collectés par Wazuh
- Au moins un scénario de détection
- Des captures d’écran du dashboard et des alertes
- Un court rapport d’incident
- Une documentation claire d’installation
- Une structure de projet prête pour GitHub

---

## 10. Description CV

**Home SOC Mini Lab — Environnement de supervision et détection d’incidents**

Mise en place d’un mini-lab SOC virtualisé avec Wazuh et des endpoints Linux afin de collecter des journaux d’authentification, détecter des tentatives de connexion SSH échouées et documenter un workflow d’investigation d’incident avec captures d’écran, étapes d’installation et rapport d’incident.

---

## 11. Statut du projet

```txt
MVP scope written: yes
Tools chosen: Ubuntu, VirtualBox, Wazuh, Ubuntu Endpoint, SSH, Linux logs
First detection scenario: Failed SSH login attempts
Repository name idea: home-soc-mini-lab
Main blocker: Installation du lab et configuration pratique encore à réaliser
```