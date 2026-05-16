# Telly
> Write-up author: Ittiwat Nimitliupanit
> 
> Category: SOC
> 
> Platform: Hack The Box Sherlocks
>
![image](./images/Telly.png)
>
## Scenario
You are a Junior DFIR Analyst at an MSSP that provides continuous monitoring and DFIR services to SMBs. Your supervisor has tasked you with analyzing network telemetry from a compromised backup server. A DLP solution flagged a possible data exfiltration attempt from this server. According to the IT team, this server wasn't very busy and was sometimes used to store backups.
>
We have 1 PCAPNG file `monitoringservice_export_202610AM-11AM.pcapng` that givien in zip file
>
1. What CVE is associated with the vulnerability exploited in the Telnet protocol?
>
We fillter need port 23 as this is a port for telnet by using `tcp.port == 23` right click and follow `TCP steam` we found the payload tha use for exploit the system `USER.-f root.DISPLAY.kali:0.0` We google and we found `CVE-2026-24061` ![link](https://www.offsec.com/blog/cve-2026-24061/)
>
> ANS: `CVE-2026-24061`
>
2. When was the Telnet vulnerability successfully exploited, granting the attacker remote root access on the target machine?
