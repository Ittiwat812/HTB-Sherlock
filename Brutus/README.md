# Brutus
> Write-up author: Ittiwat Nimitliupanit
> Category: SOC Investigation / Linux Log Analysis
> Platform: Hack The Box Sherlocks
> 

![image](./images/Brutus.png)

## Scenario
In this Sherlock, you will familiarize yourself with Unix auth.log and wtmp logs. We'll explore a scenario where a Confluence server was brute-forced via its SSH service. After gaining access to the server, the attacker performed additional activities, which we can track using auth.log. Although auth.log is primarily used for brute-force analysis, we will delve into the full potential of this artifact in our investigation, including aspects of privilege escalation, persistence, and even some visibility into command execution.

| File | Description | Purpose in Investigation |
|---|---|---|
| `auth.log` | Linux authentication log containing SSH login attempts, failed passwords, accepted logins, session activity, and sudo-related events. | Used to investigate brute-force attempts, successful authentication, affected users, source IP addresses, and attacker activity timeline. |
| `wtmp` | Binary Linux log file that records login, logout, reboot, and session information. | Used to verify successful logins and user session history. |
| `utmp.py` | Python script used to parse or analyse `wtmp`/login session data. | Used to extract readable login records from binary session files for timeline analysis. |

## Step
1. Analyze the auth.log. What is the IP address used by the attacker to carry out a brute force attack?
![image](./images/AttackerIP.png)
The `auth.log` file shows multiple failed SSH authentication attempts. In the highlighted log entries, the source IP address `65.2.161.68` repeatedly attempted to authenticate as the user `admin`.
###ANS `65.2.161.68`
3. 
4. 

```
