# Home SOC Mini Lab

> README v0 — Initial project packaging  
> Status: planning and setup phase

## Objective

**Home SOC Mini Lab** is a personal cybersecurity lab designed to practice basic Blue Team and SOC Analyst skills.

The objective is to build a small, presentable lab that can collect Linux security logs, detect suspicious activity, and document a simple incident investigation workflow.


## Lab Scope

The first version of the lab focuses on a minimal SOC setup with:

- One Wazuh Server
- One Ubuntu Endpoint
- Linux authentication logs
- SSH activity monitoring
- One clear detection scenario
- Basic incident documentation

The MVP does not aim to reproduce a full enterprise SOC.  
The priority is to build a clean, understandable, and well-documented detection workflow.

Initial lab architecture:

```txt
Ubuntu Host Machine
│
├── VM 1: Wazuh Server
│   ├── Collects logs from endpoints
│   ├── Analyzes security events
│   └── Provides a dashboard for investigation
│
└── VM 2: Ubuntu Endpoint
    ├── Generates Linux authentication logs
    ├── Runs the SSH service
    └── Sends logs to Wazuh through the Wazuh Agent
```

## Tools Planned

Main tools planned for the MVP:

- Ubuntu host machine
- VirtualBox
- Ubuntu Server VM
- Ubuntu Endpoint VM
- Wazuh Server
- Wazuh Agent
- Linux system logs
- SSH service
- Git and GitHub

Possible future tools:

- Kali Linux for attack simulation
- Wireshark for network observation
- Python for simple log parsing
- Windows VM with Sysmon
- Splunk Free for SIEM comparison

## Detection Scenario

First detection scenario:

```txt
Failed SSH login attempts / suspicious authentication logs
```

Scenario description:

An Ubuntu endpoint receives multiple failed SSH login attempts.

The failed authentication events are written into Linux authentication logs, especially:

```txt
/var/log/auth.log
```

The Wazuh Agent installed on the Ubuntu Endpoint collects the logs and sends them to the Wazuh Server.

The Wazuh Server analyzes the logs and generates alerts related to suspicious SSH authentication activity.

Expected investigation workflow:

1. Generate failed SSH login attempts against the Ubuntu Endpoint
2. Confirm the traces inside `/var/log/auth.log`
3. Check the Wazuh dashboard for related alerts
4. Capture screenshots of the alert and investigation view
5. Write a short incident report
6. Document what happened, what was detected, and what could be improved

## Current Status

```txt
MVP scope written: yes
Tools chosen: Ubuntu, VirtualBox, Wazuh, Ubuntu Endpoint, SSH, Linux logs
First detection scenario: Failed SSH login attempts
Repository name idea: home-soc-mini-lab
Lab installed: no
Wazuh Server configured: no
Ubuntu Endpoint connected: no
Detection tested: no
Main blocker: Lab installation and practical setup still need to be completed
```

## Next Steps

- [ ] Create the GitHub repository
- [ ] Install VirtualBox on Ubuntu
- [ ] Create the Wazuh Server VM
- [ ] Create the Ubuntu Endpoint VM
- [ ] Install and configure the Wazuh Agent
- [ ] Enable SSH on the Ubuntu Endpoint
- [ ] Generate failed SSH login attempts
- [ ] Verify logs in `/var/log/auth.log`
- [ ] Check alerts in the Wazuh dashboard
- [ ] Add screenshots to the repository
- [ ] Write the first incident report
- [ ] Update the README with setup steps and proof of detection

## Expected Repository Structure

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

## CV Description

**Home SOC Mini Lab — Log Monitoring & Incident Detection Environment**

Built a virtual SOC lab using Wazuh and Linux endpoints to collect authentication logs, detect failed SSH login attempts, and document a basic incident investigation workflow with screenshots, setup steps, and an incident report.

---

# Version Française

## Objectif

**Home SOC Mini Lab** est un laboratoire personnel de cybersécurité conçu pour pratiquer les bases de la Blue Team et du métier de SOC Analyst.

L’objectif est de construire un lab simple et présentable, capable de collecter des logs de sécurité Linux, détecter une activité suspecte et documenter un workflow d’investigation d’incident.


## Périmètre du lab

La première version du lab se concentre sur une configuration SOC minimale avec :

- Un serveur Wazuh
- Un endpoint Ubuntu
- Des logs d’authentification Linux
- La supervision de l’activité SSH
- Un scénario de détection clair
- Une documentation d’incident basique

Le MVP n’a pas pour objectif de reproduire un SOC complet de niveau entreprise.  
La priorité est de construire un workflow de détection propre, compréhensible et bien documenté.

Architecture initiale du lab :

```txt
Machine hôte Ubuntu
│
├── VM 1 : Wazuh Server
│   ├── Collecte les logs des endpoints
│   ├── Analyse les événements de sécurité
│   └── Fournit un dashboard pour l’investigation
│
└── VM 2 : Ubuntu Endpoint
    ├── Génère des logs d’authentification Linux
    ├── Exécute le service SSH
    └── Envoie les logs à Wazuh via l’agent Wazuh
```

## Outils prévus

Outils principaux prévus pour le MVP :

- Machine hôte Ubuntu
- VirtualBox
- VM Ubuntu Server
- VM Ubuntu Endpoint
- Wazuh Server
- Wazuh Agent
- Logs système Linux
- Service SSH
- Git et GitHub

Outils possibles pour une future extension :

- Kali Linux pour simuler des attaques
- Wireshark pour l’observation réseau
- Python pour un parsing simple des logs
- VM Windows avec Sysmon
- Splunk Free pour comparaison avec un autre SIEM

## Scénario de détection

Premier scénario de détection :

```txt
Tentatives de connexion SSH échouées / logs d’authentification suspects
```

Description du scénario :

Un endpoint Ubuntu reçoit plusieurs tentatives de connexion SSH échouées.

Les événements d’authentification échouée sont enregistrés dans les logs Linux, notamment :

```txt
/var/log/auth.log
```

L’agent Wazuh installé sur l’endpoint Ubuntu collecte les logs et les envoie au serveur Wazuh.

Le serveur Wazuh analyse les logs et génère des alertes liées à une activité SSH suspecte.

Workflow d’investigation attendu :

1. Générer des tentatives de connexion SSH échouées contre l’endpoint Ubuntu
2. Vérifier les traces dans `/var/log/auth.log`
3. Consulter le dashboard Wazuh pour trouver les alertes liées
4. Capturer des screenshots de l’alerte et de la vue d’investigation
5. Rédiger un court rapport d’incident
6. Documenter ce qui s’est passé, ce qui a été détecté et ce qui pourrait être amélioré

## Statut actuel

```txt
MVP scope written: yes
Tools chosen: Ubuntu, VirtualBox, Wazuh, Ubuntu Endpoint, SSH, Linux logs
First detection scenario: Failed SSH login attempts
Repository name idea: home-soc-mini-lab
Lab installed: no
Wazuh Server configured: no
Ubuntu Endpoint connected: no
Detection tested: no
Main blocker: Installation du lab et configuration pratique encore à réaliser
```

## Prochaines étapes

- [ ] Créer le repository GitHub
- [ ] Installer VirtualBox sur Ubuntu
- [ ] Créer la VM Wazuh Server
- [ ] Créer la VM Ubuntu Endpoint
- [ ] Installer et configurer l’agent Wazuh
- [ ] Activer SSH sur l’endpoint Ubuntu
- [ ] Générer des tentatives de connexion SSH échouées
- [ ] Vérifier les logs dans `/var/log/auth.log`
- [ ] Vérifier les alertes dans le dashboard Wazuh
- [ ] Ajouter les screenshots au repository
- [ ] Rédiger le premier rapport d’incident
- [ ] Mettre à jour le README avec les étapes d’installation et les preuves de détection
