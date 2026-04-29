OBJECTIVE

Analyze Windows Security Event Logs to identify suspicious authentication activity and possible post-access behavior.

 TOOLS USED
Windows Event Viewer
Command Prompt / PowerShell
Microsoft Windows Security Logs

 LOG SOURCES
Event ID 4625 → Failed Login
Event ID 4624 → Successful Login
Event ID 4688 → Process Creation

 EVENT ANALYSIS
1️⃣ Failed Login Attempts (Event ID 4625)
Observation
Multiple failed login attempts detected within a short time interval
Target account: user
Attempts occurred rapidly (seconds apart)
Analysis

This pattern indicates password guessing activity, commonly associated with brute-force attacks.

2️⃣ Successful Login (Event ID 4624)
Observation
A successful login event occurred shortly after multiple failed attempts
Same account involved: user
Analysis

This sequence suggests:

Failed attempts → eventual success

👉 Possible outcomes:

Correct password guessed
Legitimate user finally logged in after mistakes

⚠️ Requires correlation with other activity

3️⃣ Process Execution (Event ID 4688)
Observation
Command executed: whoami.exe
Parent process: powershell.exe
Privilege level: Elevated
Analysis

The whoami command is used to identify the current user context.

While legitimate, it is also commonly used by attackers for:

Privilege verification
Post-compromise reconnaissance

 EVENT CORRELATION
Timeline Pattern
Multiple failed logins (4625)
Successful login (4624)
Command execution (4688 – whoami)

 CORRELATED ANALYSIS

This sequence indicates a potential attack chain:

Initial access attempt (brute force)
Successful authentication
Immediate system reconnaissance

👉 This behavior is consistent with early-stage attacker activity

 RISK ASSESSMENT
Possible unauthorized system access
Account compromise risk
Potential escalation or lateral movement

 MITRE ATT&CK Mapping
Credential Access → Brute Force (T1110)
Execution → Command Execution (T1059)
Discovery → System Information Discovery (T1082)

 RECOMMENDED MITIGATION
Enforce strong password policies
Enable account lockout mechanisms
Implement Multi-Factor Authentication (MFA)
Monitor command execution from privileged shells
Alert on suspicious login patterns

 CONCLUSIONS

The analyzed logs reveal a sequence of events consistent with a simulated brute-force attack followed by reconnaissance activity.

Although this was conducted in a controlled lab environment, the pattern reflects real-world attack behavior and highlights the importance of log monitoring and correlation.

For Evidence View Screenshots in images folder below read.me



