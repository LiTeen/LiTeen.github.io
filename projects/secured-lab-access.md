# Automated Remote Lab (Kali + Tailscale + SSH)

Automated remote access setup for running Hack The Box labs on a Kali VM.

---

## Workflow

Laptop → One command SSH (Tailscale) → Home PC 

`kali-go` = start Kali linux VM Virtual box → Auto connect to HTB OpenVPN

`kali-stop` = stop Kali linux VM Virtual box

---

## What I Built

- Remote VM control via SSH over Tailscale  
- Headless Kali startup using custom PowerShell function (`kali-go` & `kali-stop`)  
- Auto-connect to HTB OpenVPN on boot  
- SSH key-based authentication (password disabled)  

---

## Why This Setup

This setup provides a stable, high-performance remote lab environment that allows for faster startups and access from anywhere.

---

## Key Implementation Details

- Tailscale used as secure network layer (no port forwarding)  
- VirtualBox for Kali VM  
- OpenSSH on Windows host  
- SSH config with key-based authentication  

---

## Issue Encountered

SSH login failed after switching to key-based authentication.

Error:
Permission denied (publickey)

---

## Investigation
https://woshub.com/using-ssh-key-based-authentication-on-windows/

Initial assumptions:
- Incorrect key placement  
- Wrong file permissions  
- User or group misconfiguration  

Verified:
- Public key exists in authorized_keys  
- Permissions are correctly set  
- User configuration is valid  

Since standard checks did not reveal the issue, I reviewed the sshd_config for conditional rules.

---

## What works for me

Comment out sshd config 
Match Group administrators  

This overrides the default key location and uses:
C:\ProgramData\ssh\administrators_authorized_keys

