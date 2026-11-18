# 🛡️ Cybersecurity Home Lab

### Building Practical Skills in SOC, Blue Team & Incident Response

![Cybersecurity](https://img.shields.io/badge/Focus-Cybersecurity-blue)
![SOC](https://img.shields.io/badge/SOC-Blue%20Team-0078D4)
![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-00A9E0)
![Linux](https://img.shields.io/badge/OS-Ubuntu%20Server-E95420)
![Status](https://img.shields.io/badge/Project-Active-success)

---

## 👨‍💻 About Me

Hi! I'm **Mikael Rodrigues Pereira**, a Cybersecurity graduate passionate about Information Security, Security Operations (SOC), Blue Team, and Incident Response.

I hold a degree in **Cybersecurity from Anhanguera** and am pursuing a postgraduate specialization in **Cyber Defense, SOC, and Incident Response at UniCesumar**.

I'm also preparing for the **CompTIA Security+ certification**, strengthening my knowledge in:

- Information Security Fundamentals
- Risk Management
- Threats and Vulnerability Management
- Security Architecture and Operations
- Security Monitoring and Threat Detection
- Incident Response
- Security Controls

I'm passionate about continuous learning and developing practical cybersecurity skills through hands-on labs, technical experiments, and simulated real-world security scenarios.

My goal is to build a professional career in cybersecurity, with a particular focus on SOC operations, security monitoring, threat detection, and incident response.

---

## 📌 About This Project

Welcome to my **Cybersecurity Home Lab**!

This repository documents the development of a self-hosted cybersecurity laboratory designed to simulate security operations and develop practical experience in defensive cybersecurity.

The environment combines physical hardware, virtualization, Linux servers, Windows systems, and security monitoring technologies.

The main objective is to develop hands-on experience with:

- Security Information and Event Management (SIEM)
- Endpoint Detection and Response (EDR)
- Security Event Monitoring
- Log Collection and Analysis
- Threat Detection and Investigation
- Incident Response
- Network Security
- Security Operations Center (SOC) Workflows

Each lab is documented to demonstrate technical implementation, troubleshooting, investigation procedures, and lessons learned.

---

## 🖥️ Lab Infrastructure

The Home Lab consists of two physical computers connected to the same local network.

### 💻 PC 1 – Main Lab Host

- **CPU:** AMD Ryzen 5 5500
- **RAM:** 16 GB
- **GPU:** 12 GB VRAM
- **Storage:** NVMe SSD
- **Host Operating System:** Windows 11 Home
- **Network Connection:** Ethernet
- **Role:** Main virtualization and security monitoring host

**Virtual Environment:**

- Virtual Machine: `SOC-SERVER-01`
- Guest OS: Ubuntu Server 24.04 LTS
- Role: Security monitoring and SIEM infrastructure
- Security Platform: Wazuh

### 💻 PC 2 – Secondary Lab Host

- **CPU:** AMD Ryzen 5 5500
- **RAM:** 16 GB
- **GPU:** 8 GB VRAM
- **Storage:** SSD
- **Host Operating System:** Windows 11 Home
- **Network Connection:** Wi-Fi
- **Role:** Secondary machine for cybersecurity experiments and endpoint testing

### 🌐 Network Environment

- Two physical computers
- Shared local network
- Ethernet and Wi-Fi connectivity
- Virtualized security monitoring environment
- Windows and Linux operating systems

---

## 🏗️ Lab Architecture

The environment uses a virtualized Ubuntu Server to host security monitoring services and support practical SOC exercises.

```text
                 INTERNET
                    |
                 ROUTER
                    |
              LOCAL NETWORK
                /       \
               /         \
              /           \
         PC 1              PC 2
       Ethernet            Wi-Fi
          |                  |
     Windows 11         Windows 11
          |
    Virtualization
          |
    SOC-SERVER-01
          |
   Ubuntu Server 24.04
          |
       Wazuh SIEM
          |
  Security Monitoring
  Log Analysis
  Alert Investigation
  Incident Detection
```

*Simplified conceptual architecture of the Home Lab.*

---

## 🛠️ Technologies & Tools

### Operating Systems

- Windows 11
- Ubuntu Server 24.04 LTS
- Linux Administration

### Security Monitoring

- Wazuh SIEM
- Security Log Analysis
- Event Monitoring
- Alert Investigation

### Infrastructure

- Virtual Machines
- Network Configuration
- SSH
- Windows Administration
- Linux Server Administration

### Security Concepts

- Security Operations Center (SOC)
- Blue Team Operations
- Endpoint Security
- Threat Detection
- Incident Response
- Vulnerability Management
- MITRE ATT&CK Framework

---

## 🎯 Learning Objectives

The primary goal of this Home Lab is to develop practical cybersecurity skills through hands-on experimentation.

**Key learning areas:**

- Configure and manage virtualized environments.
- Deploy and administer Linux servers.
- Implement security monitoring solutions.
- Collect and analyze security events.
- Investigate suspicious system activities.
- Understand endpoint security concepts.
- Practice incident detection and response.
- Improve technical troubleshooting skills.
- Document security investigations professionally.
- Develop practical SOC Analyst skills.

---

## 🧪 Practical Cybersecurity Labs

This repository includes practical exercises focused on infrastructure, monitoring, endpoint security, and incident investigation.

| Lab | Focus | Status |
|---|---|---|
| Infrastructure Setup | Physical and virtual lab configuration | Completed |
| Ubuntu Server Setup | Linux server deployment and administration | Completed |
| Wazuh SIEM Setup | Security monitoring infrastructure | Completed |
| Security Event Analysis | Log investigation and event interpretation | Completed |
| EDR Lab 03 | Endpoint security exercises | Completed |
| EDR Lab 04 | Endpoint security exercises | Completed |
| Advanced Threat Detection | Additional detection scenarios | Planned |
| Incident Response | Extended incident investigation exercises | Planned |

*Lab documentation and results are maintained as the environment evolves.*

---

## 🔍 Security Monitoring & Investigation

The laboratory is designed to provide practical exposure to SOC workflows.

### Security Event Monitoring

Using Wazuh to explore centralized security monitoring and event analysis.

### Log Investigation

Analyzing security events to understand system behavior and identify potentially suspicious activities.

### Endpoint Security

Developing practical knowledge of endpoint monitoring and defensive security operations.

### Incident Analysis

Practicing investigation techniques through controlled security scenarios.

### Documentation

Recording technical procedures, observations, screenshots, troubleshooting steps, and investigation findings.

---

## 📂 Repository Documentation

This repository is organized into dedicated sections covering infrastructure, system configuration, networking, security monitoring, and practical cybersecurity investigations.

```text
cybersecurity-home-lab/
│
├── 01-infrastructure/
│
├── 02-system-setup/
│
├── 03-networking/
│
├── 04-windows-security/
│
├── 05-security-monitoring/
│
├── 06-soc-labs/
│
├── 07-incident-response/
│
└── README.md
```

### 📚 Documentation Sections

| Directory | Description |
|---|---|
| **01-infrastructure** | Physical hardware, virtual infrastructure, and network topology. |
| **02-system-setup** | Operating system installation, configuration, and virtual machine setup. |
| **03-networking** | Network configuration, connectivity tests, and troubleshooting. |
| **04-windows-security** | Windows security settings, firewall configuration, and system hardening. |
| **05-security-monitoring** | Wazuh SIEM, log collection, security events, and monitoring. |
|
**4. Evidence**

Include screenshots, logs, commands, and relevant observations.

**5. Results**

Present the findings and explain the outcome of the experiment.

**6. Lessons Learned**

Describe the technical knowledge gained and its relevance to cybersecurity operations.

---

## 🚀 Future Improvements

The laboratory will continue evolving with additional defensive security technologies and practical exercises.

Planned areas of exploration include:

- Advanced Wazuh Monitoring
- SIEM Detection Rules
- MITRE ATT&CK Mapping
- Threat Hunting
- Incident Response Playbooks
- Active Directory Security
- Vulnerability Assessment
- Cloud Security Monitoring
- Security Automation
- Additional SOC Investigation Scenarios

---

## 🎓 Professional Development

**Academic Background**

- Cybersecurity Technology Degree — Anhanguera
- Postgraduate Studies in Cyber Defense, SOC & Incident Response — UniCesumar

**Certification in Progress**

- CompTIA Security+

**Career Interests**

- Junior SOC Analyst
- Junior Cybersecurity Analyst
- Security Monitoring Analyst
- Blue Team Analyst
- Incident Response Analyst

---

## 🎯 Project Mission

My objective is to continuously develop practical cybersecurity skills, strengthen my understanding of security operations, and build a technical portfolio that demonstrates hands-on experience.

This Home Lab represents my commitment to continuous learning, technical improvement, and professional development in Information Security.

Every experiment, configuration, and investigation contributes to my journey toward becoming a cybersecurity professional.

---

### 👨‍💻 Author

**Mikael Rodrigues Pereira**

Cybersecurity Graduate | Aspiring SOC Analyst | Blue Team Enthusiast

*Learning by doing. Detecting, investigating, and improving every day.*

---

⭐ **This repository is continuously evolving as new cybersecurity labs and projects are developed.**
