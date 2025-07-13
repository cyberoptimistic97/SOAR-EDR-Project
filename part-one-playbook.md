# 🧩 Part One: Detection-Driven Response Playbook (Draw.io)

## Objective

**This playbook demonstrates how to automate incident response using LimaCharlie and Tines. The goal is to:**
- **Receive detection events from LimaCharlie.**  
- **Automatically send a Slack message and an email alert with details of the detection.**  
- **Prompt the analyst with a "Yes or No" decision via Tines on whether to isolate the affected endpoint.**  
- **If "Yes" is selected, LimaCharlie automatically isolates the endpoint.**  
- **This workflow minimizes response time, boosts analyst efficiency, and reduces threat impact through real-time action.**


### 📊 Visual Workflow (Draw.io)
*_The below diagram, created using [draw.io](https://draw.io), illustrates the automation path from detection to decision and final containment._
.*  
[SOAR.pdf](https://github.com/user-attachments/files/20874396/SOAR.pdf)
 *This diagram shows the end-to-end automation: from detection to decision to containment.*   

 ### ⚙️ Components Used
 
- **🛡 LimaCharlie for real-time endpoint detection and response.**  
- **🤖 Tines for SOAR automation and human-in-the-loop decisions.**  
- **💬 Slack for immediate alerting to security teams.**  
- **📬 Email (SMTP) for formal alert delivery.**  
- **🖼 draw.io for creating the visual playbook flow.**  

## 🔗 Next Step

➡️ Proceed to [Part Two – LimaCharlie Setup](./part-two-edr-setup.md), where we will:
- Install the EDR agent on a Windows endpoint or VM
- Ensure it's connected and generating events
- Create a detection rule that connects to this playbook
