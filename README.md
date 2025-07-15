# SOAR-EDR-Project

## Objective

The goal of this project is to design and implement an intelligent cybersecurity automation system that integrates SOAR (Security Orchestration, Automation, and Response) with EDR (Endpoint Detection and Response) tools. This project aims to demonstrate how automated playbooks and real-time endpoint monitoring can work together to detect, investigate, and respond to security threats effectively.
By leveraging automation, this solution minimizes response time, reduces analyst fatigue, and enhances overall security posture. The project showcases a hands-on approach to modern cybersecurity defense strategies through alert handling, IP reputation checks, incident triaging, and automated containment actions.
Whether you're a cybersecurity student, SOC analyst, or automation enthusiast, this project provides a real-world demonstration of how to build smarter and faster incident response systems.



### Skills Learned

- ✅ Custom Detection & Response Rules using LimaCharlie for real-time threat identification and automated actions on endpoints.  
- 🧩 SOAR Playbook Development with Tines, integrating Slack and Email for multi-channel incident response workflows.  
- 📡 Threat Intelligence Integration and automated decision-making based on event triggers.  
- 🔗 Tool Orchestration across various platforms for streamlined and efficient security operations.  
- 🧪 Hands-on Experience simulating real-world SOC use cases and improving cyber defense readiness.  


### Tools Used

- **Telemetry generation tools** to create realistic network traffic and attack scenarios.  
- **LimaCharlie** for custom detection and automated response on endpoints.  
- **Tines** for designing SOAR playbooks and orchestrating response workflows.  
- **Slack** for real-time alert notifications and SOC collaboration.  
- **Email (SMTP)** for sending automated incident alerts.  


This project demonstrates how to build a mini SOAR system using **LimaCharlie** for detection and **Tines** for response automation. It includes real-world scenarios like detecting LaZagne execution, forwarding detections to Slack/Email, prompting analysts, and isolating endpoints.

---



## 📚 Table of Contents

| Part | Title | Description |
|------|-------|-------------|
| [Part 1](./part-one-playbook.md) | 🧩 Playbook Design | Visual workflow created using draw.io — sends Slack/Email alerts and prompts analysts. |
| [Part 2](./part-two-edr-setup.md) | 💻 Agent Setup | Installing LimaCharlie agent and verifying endpoint telemetry. |
| [Part 3](./detection-lazagne.md) | 🛡️ LaZagne Detection Rule | Create and explain detection logic for credential dumping using LaZagne. |
| [Part 4](./part-four-slack-tines-integration.md) | 📡 Slack & Tines Integration | Connect LimaCharlie → Tines → Slack/Email to automate detection alerts. |
| [Part 5](./part-five-isolation-testing.md) | 🚨 Isolation Testing | Test automated host isolation based on analyst decisions via Tines. |

---

For screenshots, refer to the `/screenshots` folder. Each Markdown part contains inline `<img>` tags with descriptions.

Let’s defend smart — automate everything. ⚙️🛡️
