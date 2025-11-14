# iRealm 🏰🔐

**iRealm** is a Kerberos-focused automation tool designed to prepare your Kali system for Active Directory interaction. It streamlines the initial setup by handling `/etc/hosts`, time synchronization, and Kerberos configuration — all in one smooth execution.

Whether you're attacking a domain in Hack The Box, TryHackMe, or conducting a real red team engagement, **iRealm** gets you domain-ready in seconds.

---

## 🛠️ Installation

### Prerequisites
In the case of installing krb5, if it asks you to enter a REALM, leave it empty and accept
```bash
sudo apt install faketime krb5-config krb5-user -y
```
## Installing the tool
```bash
wget https://raw.githubusercontent.com/Gzzcoo/iRealm/main/iRealm
chmod +x iRealm
sudo mv iRealm /usr/local/bin/iRealm
```
## ⚙️ Usage
### Interactive mode
```bash
iRealm
```
You will be prompted to enter:

  - Domain Controller IP
  - Domain name (e.g., gzzcoo.htb)
  - Hostname (e.g., dc01)

### Silent mode (no prompts)
```bash
iRealm --force <IP> <DOMAIN> <HOSTNAME>
```
Example:
```bash
iRealm --force 10.10.10.10 gzzcoo.htb dc01
```

## 🚀 Features

  - Adds the Domain Controller and domain name to /etc/hosts.
  - Synchronizes your system time with the Domain Controller to prevent Kerberos clock skew issues.
  - Replaces /etc/krb5.conf with a valid Kerberos configuration.
  - Creates an automatic backup of your previous Kerberos config.
  - Supports both interactive and non-interactive modes.

## 📌 Why use iRealm?

Working in Active Directory environments often requires Kerberos to be properly configured — and misconfigurations can cause tools like GetNPUsers, GetUserSPNs, or psexec.py to fail silently.

**iRealm** ensures your box is ready for action with:

  - Correct DNS resolution to the DC
  - Accurate system time
  - Valid Kerberos realm configuration

## 📸 Preview

https://github.com/user-attachments/assets/4d3d969e-31d8-4393-a39e-9547fd21afaf



[![asciicast](https://asciinema.org/a/IGU4IZacmaieu5oeXnR3ajk8j.svg)](https://asciinema.org/a/IGU4IZacmaieu5oeXnR3ajk8j)




<a href="https://asciinema.org/a/IGU4IZacmaieu5oeXnR3ajk8j" target="_blank"><img src="https://asciinema.org/a/IGU4IZacmaieu5oeXnR3ajk8j.svg" /></a>
