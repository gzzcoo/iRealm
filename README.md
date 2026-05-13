# iRealm 🔐

**iRealm** is a Kerberos-focused automation tool designed to prepare your Linux system for Active Directory interaction. It streamlines the initial setup by handling `/etc/hosts` cleaning, time synchronization, and Kerberos configuration — all in one smooth execution.

Whether you're attacking a single domain or pivoting through complex cross-forest trusts in environments like Hack The Box (HTB) or real engagements, **iRealm** gets your tools domain-ready in seconds.

---

## 🛠️ Installation

### Prerequisites
In the case of installing krb5, if it asks you to enter a REALM, leave it empty and accept.
```bash
sudo apt install faketime rdate krb5-config krb5-user -y
```

### Installing the tool
```bash
wget [https://raw.githubusercontent.com/Gzzcoo/iRealm/main/iRealm](https://raw.githubusercontent.com/Gzzcoo/iRealm/main/iRealm) -O iRealm
chmod +x iRealm
sudo mv iRealm /usr/local/bin/iRealm
```

## ⚙️ Usage

iRealm uses explicit flags for better stability and control. You can view all options at any time using `iRealm --help`.

### Interactive Mode
Simply run the tool without arguments to enter the interactive setup:
```bash
iRealm
```
You will be prompted to enter the Target IP, Domain, Hostname, and choose whether to configure an additional cross-forest trust or sync the DC time.

### Non-Interactive (Silent) Mode
Perfect for quick executions or aliases. Use the `--force` flag along with `-i`, `-d`, and `-n`.
```bash
iRealm -i 10.10.10.10 -d inlanefreight.ad -n DC01 --force
```

### Cross-Forest Setup
If you are adding a child domain or pivoting across a forest trust, use the `--cross-forest` flag. This safely **appends** the new realm to your existing `/etc/krb5.conf` using `awk` instead of overwriting your parent domain config!
```bash
iRealm -i 172.16.10.3 -d megacorp.ad -n DC01 --cross-forest --force
```

### Optional Time Sync
Add `--sync-time` to automatically fetch the DC's time using `rdate` and drop you into an isolated `faketime` subshell. This prevents Kerberos clock skew errors without messing with your host's actual clock.
```bash
iRealm -i 10.10.10.10 -d inlanefreight.ad -n DC01 --sync-time --force
```

## 🚀 Features

  - **Smart `/etc/hosts` Management:** Uses case-insensitive regex to find and clean up previous malformed manual entries before adding the correct IP, FQDN, and hostname.
  - **Cross-Forest Support:** Safely injects new realms into existing Kerberos configurations without destroying existing setups.
  - **Container Safe:** Engineered to bypass the classic `Device or resource busy` error on bind mounts, making it **fully compatible with Docker and Exegol environments**.
  - **Kerberos Clock Sync:** Automates DC time fetching and isolates the time spoofing inside a subshell.
  - **Failsafe Backups:** Creates an automatic backup of your previous Kerberos config (`/etc/krb5.conf.bak`).

## 📌 Why use iRealm?

Working in Active Directory environments often requires Kerberos to be properly configured — and misconfigurations can cause tools like NetExec, GetNPUsers, bloodyAD, or psexec.py to fail silently.

**iRealm** ensures your box is ready for action with:
  - Correct DNS resolution to the DC
  - Accurate system time alignment
  - Valid and structured Kerberos realm configuration
