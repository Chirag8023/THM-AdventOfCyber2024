<table border=4><tr><th colspan=2>
  
# Advent Of Cyber 2024 🎄
Just a memoir of the challenges

</th></tr><tr><th>Day</th><th>Challenge</th></tr>
<tr><th>1.</th><td>

## OPSEC ( Purple Teaming )
We explored a YouTube-to-MP3 website which was installing malware to it's users and analyze the meta-data of the malware through that we back trace to the attacker's actual identity. 

- **Commands & Tools Used :** Find, Exiftool, Github.
<br>
</td></tr>

<tr><th>2.</th><td>
  
## Log Analysis ( Blue Teaming )
We Investigated security logs of a website and find pattern in the authentication and detected a brute force attack then examine the encoded powershell command that has been run on the systems.

- **Commands & Tools Used :** Elastic SIEM, CyberChef.
<br>
</td></tr>

<tr><th>3.</th><td>


## Log Analysis ( Purple Teaming )
This time We used ELK to search through logs and findout a specific ip which was using a web shell through profile picture upload and in second half We log into a website as admin because of weak/common credentials and try to exploit a RCE via file upload. 

- **Commands & Tools Used :**  ELK (Elasticsearch, Logstash, and Kibana), ls, cat.
- **Techniques Used :** RCE (Remote Code Execution).
<br>
</td></tr>

<tr><th>4.</th><td>

## Atomic Red Team ( Purple Teaming )
We recreated MITRE ATT&CK technique `T1566.001 Spearphishing` using the Atomic Red Team library, then in Windows Event Logs analyze Sysmon logs confirming the compromise. Next, We tested technique `T1059.003 Command and Scripting Interpreter: Windows Command Shell`, after iterating through multiple test we found the one from which the machine was vulnerable to.

- **Commands & Tools Used :** Atomic Red Team Library, Sysmon, Windows Event Logs.
<br>
</td></tr>

<tr><th>5.</th><td>

## XXE ( Red Teaming )
We used the `Burp Suite` to intercept request and response and try to findout if the website is vulnerable to XXE(XML external entity) Injection then exploit it to get data only admins can access.

- **Commands & Tools Used :** Burp Suite.
- **Techniques Used :** XXE(XML external entity) Injection.
<br>
</td></tr>

<tr><th>6.</th><td>

## Sandboxes ( Blue Teaming )
We tested a malware in virtual machine and detect it with `YARA rules` after getting detected we obscure it by using encoded commands, but it was still detectable by `floss` and `sysmon logs`.

- **Commands & Tools Used :** YARA, Sysmon, CyberChef, FLOSS.
<br>
</td></tr>

<tr><th>7.</th><td>

## AWS Log Analysis ( Blue Teaming )
We went through amazon cloudtrail and rds logs using `jq` and `grep` to find out who actually responsible for altering the qr code on donation website.

- **Commands & Tools Used :** JQ, grep.
<br>
</td></tr>

<tr><th>8.</th><td>

## Shellcodes ( Purple Teaming )
Using `msfvenom` we generate a shellcode then try to achieve a reverse shell by executing that to the target machine by loading it to memory.

- **Commands & Tools Used :** msfvenom, nc.
<br>
</td></tr>

<tr><th>9.</th><td>

## GRC ( Blue Teaming )
We perform a Risk Assessments based on the questions answerd by different vendors to choose the one with lowest risk.

<br>
</td></tr>

<tr><th>10.</th><td>

## Phishing ( Red Teaming )
We use `Metasploit Framework` to create a malicious macro and sent it through similar looking email and when the macro file opend we got access to the target system.

- **Commands & Tools Used :** Metasploit Framework.
- **Techniques Used :** typosquatting.
<br>
</td></tr>

<tr><th>11.</th><td>

## Wi-Fi attacks ( Red Teaming )
We got into monitor mode using `iw dev`, then use `airodump-ng` to scan for nearby networks, capture the 4 way handshake by sending deauth packets to specific BSSID then crack the password using `aircrack-ng` dictionary attack on the captured handshake file.

- **Commands & Tools Used :** iw, airodump-ng, aircrack-ng, aireplay-ng.
<br>
</td></tr>

<tr><th>12.</th><td>

## Web timing attacks ( Red Teaming )

<br>
</td></tr>

<tr><th>13.</th><td>

## Websockets ( Red Teaming )

<br>
</td></tr>

<tr><th>14.</th><td>

## Certificate mismanagement ( Red Teaming )

<br>
</td></tr>

<tr><th>15.</th><td>

## Active Directory ( Blue Teaming )

<br>
</td></tr>
<tr><th>16.</th><td>

## Azure ( Red Teaming )

<br>
</td></tr>
<tr><th>17.</th><td>

## Log analysis ( Blue Teaming )

<br>
</td></tr>
<tr><th>18.</th><td>

## Prompt injection ( Red Teaming )

<br>
</td></tr>
<tr><th>19.</th><td>

## Game Hacking ( Red Teaming )

<br>
</td></tr>
<tr><th>20.</th><td>

## Traffic analysis ( Blue Teaming )

<br>
</td></tr>
<tr><th>21.</th><td>

## Reverse engineering ( Blue Teaming )

<br>
</td></tr>
<tr><th>22.</th><td>

## Kubernetes DFIR ( Blue Teaming )

<br>
</td></tr>
<tr><th>23.</th><td>

## Hash cracking ( Red Teaming )

<br>
</td></tr>
<tr><th>24.</th><td>

## Communication protocols ( Blue Teaming )

<br>
</td></tr>

</table>
