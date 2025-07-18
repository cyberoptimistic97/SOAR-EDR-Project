# 📡 Part 4: Slack & Tines Integration

## 🎯 Objective

To integrate **Slack** and **Tines** into the LimaCharlie detection pipeline for automated alerting and analyst interaction.

This step ensures that:
- Detections from LimaCharlie are forwarded to Tines via webhook
- Tines sends real-time notifications to **Slack** and **Email**
- Analysts can review and respond to threats quickly

---

## 🔧 Step 1: Set Up Slack Webhook

1. Go to your [Slack App Directory](https://api.slack.com/apps)
2. Create a new **Incoming Webhook**
3. Choose a target channel (e.g., `#security-alerts`)
4. Copy the **Webhook URL**

### ➕ In Tines:
- Create a new action: **Send to Slack**
- Paste your **Webhook URL**
- Format your message payload:

```json
{
  "text": "🚨 *Detection Alert from LimaCharlie* 🚨\n• *Rule:* LaZagne Detected\n• *Host:* WIN-TEST01\n• *Time:* 2025-06-24 12:15 UTC\n• *Action Required:* Analyst Review"
}
```
## 🔗 Step 2: Connect LimaCharlie to Tines

1. In **Tines**, create a new **Webhook Action** to receive incoming JSON data.
2. Copy the **Webhook URL** generated by Tines.

### ➡️ In LimaCharlie:

- Navigate to `Outputs` → click **Add Output**
- Select **Webhook** as the output type
- Paste the **Tines Webhook URL**
- Under **Event Types**, choose:
  - `report`
  - `detection`
  - `event`

✅ This configuration ensures all relevant detection data from LimaCharlie is automatically forwarded to Tines in real-time for automated response.

## 🔁 Step 3: Test the Integration

To verify everything is working correctly, follow these steps:

1. Trigger your detection — for example, by running `LaZagne.exe` on your Windows test machine.

2. Confirm the following response flow:

- ✅ **LimaCharlie** detects and logs the event
- ✅ **Tines** receives the detection via its Webhook
- ✅ A **Slack message** is posted in the target alert channel
- ✅ An **Email notification** is sent (if configured in Tines)
- ❓ **Prompt to Analyst**: _"Do you want to isolate this host?"_

3. Based on the analyst’s response:

- **Yes** ✅  
   → Tines sends an API command to **LimaCharlie**  
   → The endpoint is **isolated** from the network

- **No** ❌  
   → The decision is **logged for auditing**  
   → No isolation is performed  
   → Optional: Send follow-up alert to escalate or monitor the host

> 📌 Both responses help simulate real-world SOC decision-making and incident handling.

Malicious Activity Detected → LimaCharlie Rule Fires → Tines Webhook Triggered → Slack & Email Alerts Sent → Analyst Prompted → (Optional) Host Isolated

## 🔜 Next Step

Proceed to [**Part Five: Isolation Workflow Testing**](./part-five-isolation-testing.md) to simulate the complete SOAR response cycle:


This final part ensures your playbook not only detects threats but also responds to them automatically, reducing response time and analyst fatigue.
