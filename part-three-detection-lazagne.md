# 🧪 Part Three: Detecting LaZagne Activity and Automating Response

## 🎯 Objective

In this part of the project, the goal is to:
- Generate telemetry related to **LaZagne**, a known password recovery tool
- Create a **Detection & Response Rule** in **LimaCharlie** to detect this suspicious activity
- Automatically forward the detection to **Tines** to trigger a response workflow (Slack alert, email, and possible endpoint isolation)

---

## 1️⃣ Simulate LaZagne Activity

### 🧰 Tool Used: LaZagne

[LaZagne](https://github.com/AlessandroZ/LaZagne) is a post-exploitation tool that extracts credentials from Windows machines.

📌 **Important Note**:  
Use this tool **only in a safe test environment** like a **Windows VM**. Do **not** run LaZagne on production systems.

### ▶️ Steps to Simulate:

1. Download the LaZagne executable on the test machine.
2. Open **PowerShell or CMD** as Administrator.
3. Navigate to the folder where LaZagne is located:

    ```bash
    cd Downloads
    ```

4. Run LaZagne:

    ```bash
    LaZagne.exe all
    ```

✅ This action will generate process telemetry, including the file name and command line string.

---

## 2️⃣ Create Detection & Response Rule in LimaCharlie

### 📌 Detection Rule – `Detect LaZagne Execution`

In LimaCharlie, go to **Detections → Add Rule** and paste the following YAML:

### 🛡️ Detection Rule: MyDFIR - HackTool - Lazagne

```yaml
events:
  - NEW_PROCESS
  - EXISTING_PROCESS
op: and
rules:
  - op: is windows
  - op: or
    rules:
      - case sensitive: false
        op: ends with
        path: event/FILE_PATH
        value: LaZagne.exe
      - case sensitive: false
        op: contains
        path: event/COMMAND_LINE
        value: LaZagne
      - case sensitive: false
        op: is
        path: event/HASH
        value: '3cc5ee93a9ba1fc57389705283b760c8bd61f35e9398bbfa3210e2becf6d4b05'

- action: report
  metadata:
    author: CyberOptimistic97
    description: TEST - Detects Lazagne Usage
    falsepositives:
      - ToTheMoon
    level: high
    tags:
      - attack.credential_access
  name: CyberOptimistic97 - HackTool - Lazagne
```
This detection rule monitors Windows processes for any signs of LaZagne execution. It identifies LaZagne based on:
- The executable name (LaZagne.exe)
- The command-line arguments
- The known SHA256 hash of the binary

Once detected, it reports the activity and forwards it to Tines for automation, which may include notifying analysts or isolating the affected endpoint.

---

## 📘 Next Step: Send Detection to Tines

Once this detection rule is triggered, LimaCharlie will forward the alert to **Tines** for automation.

Tines will:
- Notify the SOC team via **Slack** and **Email**
- Prompt the analyst with a **Yes/No isolation decision**
- Automatically isolate the machine using LimaCharlie if "Yes" is selected

Make sure your Tines workflow is active and properly integrated with your LimaCharlie organization.

➡️ [Go back to Part One](./part-one-playbook.md) or [Proceed to Part Four](./part-four-isolation-response.md) for deeper automation logic.

---
