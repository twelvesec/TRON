<p align="center">
</p>

<h1 align="center">🏴‍☠️ TRON</h1>
<p align="center">
  <b>Windows Trojan & Reverse-Shell Generator Tool</b><br>
  <i>AV/AMSI evasion</i>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/version-v1.7.5-blue.svg" alt="Version">
  <img src="https://img.shields.io/badge/language-bash-green.svg" alt="Bash">
  <img src="https://img.shields.io/badge/language-rust-orange.svg" alt="Rust">
  <img src="https://img.shields.io/badge/language-powershell-blueviolet.svg" alt="PowerShell">
</p>

---


## 📖 About

**TRON** is a hacking tool designed to deploy **Windows reverse cmd, PowerShell, and Meterpreter shells** utilizing AMSI and AV evasion techniques.

Originally developed for internal penetration tests, TRON was built to reliably bypass antivirus controls and establish reverse shells during authorized assessments. **TwelveSec** recently recovered this tool from their archives and is publishing it for the security community to use for research, education, and fun.❤️

---

## ⚙️ Instalation/Usage

```
git clone https://github.com/twelvesec/TRON.git
sudo ln -s $(pwd)/TRON/tron /usr/bin/
sudo tron
```
---

## 💻 Supported Operating Systems

TRON currently supports the following platforms:

* **Kali Linux** (ARM64 & AMD64)
* **Debian**
* **Parrot OS**

---

## ✨ Features

TRON provides several shell-generation and execution techniques.

### Evasion-Oriented Simple Shell

```text
0. Simple PowerShell shell (stageless)
```

### AMSI Crasher Techniques

```text
1. Simple CMD shell (staged)
2. Meterpreter reverse_https shell (staged)
3. Meterpreter reverse_tcp shell (staged)
4. Meterpreter encrypted reverse_tcp shell (encrypted_staged)
5. Meterpreter win_https shell (staged)
```

### New Age Techniques

```text
6. Simple CMD command executor
7. Meterpreter reverse_https shell (Under Development)
```

## 🛡️ AV evasion

**Test date:** `23/09/2026`

TRON was tested against a fully updated Windows 11 installation with Microsoft Defender enabled.

https://github.com/user-attachments/assets/e2a11089-c6eb-411e-bbb8-b569ed452962

🔊 ***We strongly encourage the community to test TRON against various AV solutions across different environments. Feel free to share your testing results, report bugs, or open issues on GitHub or social media so we can continue updating and improving the tool.***

---

## 🌐 HTTP Server

The generated executable expects to retrieve the required PowerShell components and payload-related files from an HTTP server.

The current implementation expects the HTTP server to listen on:

```text
TCP/80
```

The server should serve the directory containing the generated files.

For example:

```bash
sudo python3 -m http.server 80
```

## 🏗️ How It Works

TRON utilizes a staged delivery architecture that requires two open ports on the operator's machine:
1. **HTTP Server (Port 80):** Serves the necessary staging files and decryption keys.
2. **Reverse Shell Listener (Custom Port):** Catches the incoming connection from the executed payload.

When the generated executable is run on the target machine, it reaches out to the operator's HTTP server and downloads three specific files:
- A PowerShell script that crashes AMSI.
- A PowerShell script containing the encrypted reverse shell payload.
- A text file containing the exact passphrase required for decryption.

Once downloaded, the payload is decrypted in memory and executed, establishing a reverse shell connection back to the operator's listening port.

### Architecture Flow

```text
                 ┌─────────────────────────────────────────┐
                 │           Attacker Infrastructure       │
                 │                                         │
                 │  ┌──────────────┐      ┌─────────────┐  │
                 │  │ HTTP Server  │      │   Listener  │  │
                 │  │   (TCP/80)   │      │ (Custom TCP)│  │
                 │  └──────┬───────┘      └──────▲──────┘  │
                 └─────────┼─────────────────────┼─────────┘
                           │                     │
      1. Executable requests staging files       │ 3. Decrypted payload
                           │                     │    connects back
                           ▼                     │
                 ┌─────────┴─────────────────────┼─────────┐
                 │           Target Machine      │         │
                 │                               │         │
                 │  2. Downloads:                │         │
                 │  ├── Amsi Crasher PS Script   │         │
                 │  ├── Encrypted PS Payload     │         │
                 │  └── Decryption Key File      │         │
                 │                               │         │
                 └───────────────────────────────┴─────────┘
```

## 🗺️ ToDo / Roadmap

- [ ] Add an offline mode (skip update checks if the host lacks internet access).
- [ ] Implement a ZIP packer option for payloads.
- [ ] Implement an ISO packer option for payloads.
- [ ] Develop new undetectable (FUD) Meterpreter evasion techniques.

---

## 👨‍💻 Credits

TRON was originally created by **Aristos** for internal penetration-testing activities.
The project was subsequently recovered from an archive and released by **TwelveSec** for the security community.
```text
Made by Aristos with Love ♥
```
---

## ⚠️ Disclaimer

Only use TRON against systems for which you have **explicit authorization**.
The authors and contributors are not responsible for unauthorized use, damage, or other consequences resulting from the use of this software.

---

## 📜 License

TRON is released under the MIT license. See LICENSE for details.
