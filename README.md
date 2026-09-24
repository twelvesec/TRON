# Tron Trojan Generator

#### -> Version 1.4.4

### Small Description

The program will **generate** four files: **two PowerShell scripts**, **one file** that contains the **encryption words**, and **one executable** that will be sent to the victim.

We need to set up an HTTP server on port 80 because our executable will request the encryption keys and the PowerShell scripts from it. 

<u>Therefore, it is essential to run an HTTP server on port 80 in the directory where these files are located.</u>

## Supported OS

- Kali Linux (Arm64)
- Kali Linux (Amd64)

## ToDo Checklists (Implemented/predicted version)

- [x] Create a simple reverse shell
- [x] Set up the ApacheSerer (v1.1)
- [x] ip choose also with number (v1.2)
- [x] auto-copy the final command (v1.3) 
- [x] random variables (v1.4) 
- [x] variable name from a wordlist (v1.4.2)
- [ ] Moving banner (v1.4.4)
- [ ] Fix encrypted_shell from msfvenom
- [ ] Set Up ssl communication (v1.9)
- [ ] Set up trusted domain

### Bugs

- [x] After listing the IPs of the system, it creates new line (v1.2)