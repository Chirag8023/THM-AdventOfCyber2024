# Advent Of Cyber 2024 🎄
Just a memoir of the challenges

## Day 01 (OPSEC - Purple Teaming)
We explored a YouTube-to-MP3 website which was installing malware to it's users and we analyze the meta-data of the malware through that we back trace to the attacker's actual identity. 

- **Commands & Tools Used :** Find, Exiftool, Github.

## Day 02 (Log Analysis - Blue Teaming)
We Investigated security logs of a website and find pattern in the authentication and detected a brute force attack then examine the encoded powershell command that has been run on the systems.

- **Commands & Tools Used :** Elastic SIEM, CyberChef.

## Day 03 (Log Analysis - Purple Teaming)
This time we used ELK to search through logs and findout a specific ip which was using a web shell through profile picture upload and in second half we log into a website as admin because of weak/common credentials and try to exploit a RCE via file upload. 

- **Commands & Tools Used :** . ELK (Elasticsearch, Logstash, and Kibana), ls, cat.
- **Techniques Used :** RCE (Remote Code Execution).
