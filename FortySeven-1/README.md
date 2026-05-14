# FortySeven-1
> Write-up author: Ittiwat Nimitliupanit
> 
> Category: Threat Intelligence
> 
> Platform: Hack The Box Sherlocks

![image](./images/FortySeven-1.png)

## Scenario
An APT group is using Hajj-themed phishing lures to target and steal WhatsApp data from government and diplomatic officials. Our team has gathered fragmented intelligence from public cybersecurity vendor reports, blog posts, and internal security alerts. Your task is to build a comprehensive profile of the threat actor responsible. You must connect the dots between different reports to answer questions about their identity, tools, and motives.
>
Below are the sites we have compiled, use these to answer the following questions. (If any of the sites become unavailable please check on wayback machine as they all have been saved).
>
Evidence - 1 - https://securelist.com/mysterious-elephant-apt-ttps-and-tools/117596/ Evidence - 2 - https://medium.com/@knownsec404team/apt-k-47-mysterious-elephant-a-new-apt-organization-in-south-asia-5c66f954477 Evidence - 3 - https://medium.com/@knownsec404team/unveiling-the-past-and-present-of-apt-k-47-weapon-asyncshell-5a98f75c2d68
>

## Step
1. What is the primary name of the APT group described in the SecureList report?
>
Access to the Evidence - 1 - https://securelist.com/mysterious-elephant-apt-ttps-and-tools/117596/ and we found in first paragraph.
![image](./images/PrimarynameAPT.png)
>
> Ans: `Mysterious Elephant`
>
2. According to the Knownsec 404 team's analysis(Evidence -3), since which year has this group's attack activity been dated back to?
>
Access to Evidence - 3 Evidence - 3 - https://medium.com/@knownsec404team/unveiling-the-past-and-present-of-apt-k-47-weapon-asyncshell-5a98f75c2d68
![image](./images/dateback.png)
>
> Ans:  `2022`
>
3. The group uses a custom backdoor that communicates via Office Remote Procedure Call (ORPCBackdoor). According to the Knownsec 404 team's analysis(Evidence -2), what is the name of the first malicious exported entry function?
>
Access to Evidence - 2 https://medium.com/@knownsec404team/apt-k-47-mysterious-elephant-a-new-apt-organization-in-south-asia-5c66f954477 take a look to the Overview of sample functions
![image](./images/firstscript.png) 
>
> ANS: `GetFileVersionInfoByHandleEx(void)`
>
4. The previously mentioned backdoor checks for a file before creating persistence. What is the name of the file?
>
Access to Evidence - 2 https://medium.com/@knownsec404team/apt-k-47-mysterious-elephant-a-new-apt-organization-in-south-asia-5c66f954477 take a look to the persistance section
![image](./images/checkfile.png)
>
> ANS: `ts.dat`
>
5. The use of the backdoor links the APT to another well-known South Asian APT group. What is the name of this other group?
>
Access to Evidence - 2 https://medium.com/@knownsec404team/apt-k-47-mysterious-elephant-a-new-apt-organization-in-south-asia-5c66f954477 take a look to the persistance section
![image](./images/othergroup.png)
>
> ANS: `BITTER`
>
6. The APT group we are currently investigating has consistently used and updated another backdoor since 2023, with its C2 communication evolving from TCP to HTTPS. What is the name of this tool?
>
Access to Evidence - 3 - https://medium.com/@knownsec404team/unveiling-the-past-and-present-of-apt-k-47-weapon-asyncshell-5a98f75c2d68 take a look to the transition from tcp to https
![image](./images/tcptohttp.png)
>
> ANS: `Asyncshell-v2`
>
7.  To evade sandbox analysis, the MemLoader HidenDesk tool checks the number of active processes before running. What is the minimum number of processes required for it to proceed?
>
Access to the Evidence - 1 - https://securelist.com/mysterious-elephant-apt-ttps-and-tools/117596/ and we found in Customized open-source tools section.
>
![image](./images/MemLoader.png)
>
> ANS:  `40`
>
8. The MemLoader HidenDesk tool creates a covert environment for its activities by creating and switching to a specific environment. What is the name of this hidden desktop?
>
We use the same figure as question 7 to get the answer.
> ANS:  `MalwareTech_Hidden`
>
9. The MemLoader HidenDesk tool achieves persistence by placing a shortcut in the autostart folder to ensure it runs after a system reboot. What is the MITRE ATT&CK ID for the 'Registry Run Keys / Startup Folder' technique?
>
Google
> ANS:  `T1547.001`
>
10. The actor uses several custom exfiltration tools targeting WhatsApp. What is the name of the tool that recursively searches specific directories, including the “Desktop” and “Downloads” folders?
>
Found in Evidence - 1 - https://securelist.com/mysterious-elephant-apt-ttps-and-tools/117596/ in WhatsApp-specific exfiltration tools section.
> ANS:  `Stom Exfiltrator`
>
11. Kaspersky's analysis highlights the actor's heavy use of scripts for execution and deploying payloads. What is the MITRE ATT&CK ID for the 'PowerShell' technique?
>
Google
> ANS:  `T1059.001`
>
12. In their early attack chains, Mysterious Elephant used a downloader that was previously associated with the Origami Elephant group. What was the name of this downloader?
>
Found in Evidence - 1 - https://securelist.com/mysterious-elephant-apt-ttps-and-tools/117596/ in The emergence of Mysterious Elephant section.
> ANS:  `Vtyrei`
>
13. In a January 2024 campaign delivering an Asyncshell payload, which CVE was exploited in the malicious archive file?
>
Google
> ANS:  `CVE-2023-38831`
>
14. What is the MD5 hash of the ChromeStealer Exfiltrator sample named WhatsAppOB.exe?
>
Found in Evidence - 1 - https://securelist.com/mysterious-elephant-apt-ttps-and-tools/117596/ in File hashes
> ANS:  `9e50adb6107067ff0bab73307f5499b6`
>
15. The intelligence describes multiple custom tools designed to upload stolen data to the actor's servers. According to the MITRE ATT&CK framework, what is the ID for the 'Exfiltration Over C2 Channel' technique?
>
Google
> ANS:  `T1041`
>
