# Information Disclosure Vulnerability Exploitation in Web Applications – Exposed Backup File Reveals Source Code and Credentials

## Overview  
While performing file and directory enumeration, I discovered an exposed backup file on the server containing raw source code. Inside the archive, I found hardcoded credentials and API keys—granting direct access to sensitive backend services.

## Proof of Concept (PoC)  
I ran directory brute-forcing on the target using a common wordlist and found `/backup.zip` accessible without authentication. After downloading and extracting it, I located the full application source code, including `.env` and configuration files.  

The `.env` file contained:
- Database credentials  
- SMTP server access  
- Private API keys for third-party services

Tools used:
- Dirsearch (to find hidden files and folders)
- wget/unzip (to extract the archive)
- Manual review of configuration files

## Deductions  
This vulnerability resulted from:
- Leaving sensitive backup files exposed in the web root
- Lack of file access controls
- No automatic cleanup or protection of environment files

To mitigate:
- Never store backups in publicly accessible directories
- Use `.gitignore`, `.htaccess`, or WAF rules to block sensitive file access
- Store environment secrets outside of application directories

Accidentally exposed backups are low-effort discoveries with high-impact consequences.


<details>
<summary>Click to view screenshots</summary>

**Screenshot 1: Error page revealing internal path**  
![Screenshot 1](<https://i.imgur.com/QJCjrnB.jpg>)

**Screenshot 2: Debug info exposed in response headers**  
![Screenshot 2](<https://i.imgur.com/zkfKLOt.jpg>)

**Screenshot 3: Sensitive email addresses leaked**  
![Screenshot 3](<https://i.imgur.com/S2cGjWq.jpg>)

</details>

> **Disclosure:** *To protect the confidentiality of client systems, representative lab screenshots demonstrating identical exploitation techniques have been used instead of actual client environment visuals.*


