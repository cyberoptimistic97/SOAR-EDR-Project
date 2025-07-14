# 🛡️ Part 5: Isolation Workflow Testing

## 🎯 Objective

This stage validates the **full response loop** — from threat detection to endpoint isolation. When a detection is triggered, analysts are prompted to act, and the endpoint is **automatically isolated** if approved.

---

## 🔁 Workflow Overview


```text
```
1. Malicious behavior occurs (e.g., LaZagne execution)
2. LimaCharlie detects and triggers the rule
3. Tines receives the detection via Webhook
4. Slack and Email alerts are sent to the SOC team
5. Analyst receives a Yes/No prompt in Tines:
   - ✅ Yes → LimaCharlie isolates the endpoint
   - ❌ No → Action is logged and monitoring continues

## ⚙️ Tools Involved

| Tool                | Purpose                                                                 |
|---------------------|-------------------------------------------------------------------------|
| **LimaCharlie**     | Endpoint detection, event collection, and isolation control             |
| **Tines**           | SOAR automation: alert routing, analyst prompt, and decision-making     |
| **Slack / Email**   | Channels for sending alerts and analyst notifications                   |
| **Windows Endpoint**| Simulated host used for generating real attack behavior (e.g., LaZagne) |

## 🧪 Testing Procedure

### ✅ Step 1: Simulate an Attack

Run `LaZagne.exe` or another known malicious executable on your test Windows system to trigger the detection rule in LimaCharlie.

---

### ✅ Step 2: Observe the Response Flow

Once triggered, verify the following sequence:

- ✅ **LimaCharlie** logs the detection and matches the rule
- ✅ **Tines** receives the alert and starts the SOAR workflow
- ✅ **Slack** and **Email** receive alert notifications
- ✅ **Tines** prompts the analyst with:
  > “Do you want to isolate this host?”

---

### ✅ Step 3: Analyst Makes a Decision

#### ➤ If "Yes":
- **Tines** sends a `sensor.isolate()` command to LimaCharlie via API  
- The host is automatically **isolated**  
- Isolation status can be verified in the LimaCharlie dashboard

#### ➤ If "No":
- The analyst's decision is **logged** in Tines  
- No isolation is performed  
- Optional: Escalate or continue monitoring the host

---

### 🔒 Confirm Isolation in LimaCharlie

Go to:

`LimaCharlie Console → Sensors → [Your Endpoint]`
---

- ✅ The sensor status should now display: **“Isolated”**
- All outbound network activity from that endpoint should be **blocked**

> Isolation ensures the threat is contained while analysts investigate further.
