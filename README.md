# Enabler-Ops

**Enabler-Ops** is a utility designed to automate the process of enabling the Local Administrator account, configuring Remote Desktop Protocol (RDP), and adding the Administrator account to specific RDP group locally. This tool is designed with operational security (OpSec) in mind, minimizing detection during red team exercises by avoiding excessive process creation and command-line logging.

---

## **Features**
- Enables the Local Administrator account and sets a custom password.
- Configures RDP access (enables RDP in the registry and through the Windows Firewall).
- Adds the Local Administrator account to **Remote Desktop Users** and **Administrators** groups.
- Bypasses common detection points by leveraging Windows APIs instead of system commands like `net user`, `reg`, and `sc`.

---

## **Why This Tool is OpSec-Safe**
This tool avoids traditional process creation that can leave artifacts in command-line history, Windows Event Logs, and process creation logs often monitored by Endpoint Detection and Response (EDR) systems. The following measures are taken to ensure stealth:

1. **Windows APIs instead of Commands**:
   - **Account modification** uses `NetUserSetInfo` API instead of `net user`.
   - **Registry edits** are performed using `Microsoft.Win32.Registry`.
   - **Service management** is handled through the `ServiceController` class instead of `sc` commands.

2. **Minimal Process Creation**:
   - Only the firewall rule update uses a system command (`netsh`), which can be easily modified to use a firewall management API.

3. **Reduced Logs and Artifacts**:
   - No `cmd.exe` or command-line tools (`net`, `sc`, `reg`) are used to enable/modify the account or services.
   - The code directly manipulates system components through API calls, bypassing common monitoring points like Windows Event Logs for `cmd` or `net` usage.

---

## **Setup Instructions**
1. Clone this repository:
   ```sh
   git clone https://github.com/sheb1853/enabler-ops.git

