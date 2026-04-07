# Automated Remote Lab (Kali VM + Tailscale + SSH)

An automated workflow for remote Hack The Box labs, designed to instantly link my laptop to a home-based Kali VM. This setup handles all networking and OpenVPN services, providing one-command access to my high-performance desktop from any location.


 
>### Workflow

Laptop → one-command  → Home desktop 

`kali-go` = start Kali linux VM → SSH connect to kali → Auto connect to HTB OpenVPN

`kali-stop` = end Kali linux VM 



## What I Built

- Tailscale used as secure network layer (no port forwarding)  
- Remote VirtualBox control via SSH over Tailscale  
- Auto-connect to HTB OpenVPN on every boot up 
- Deploy SSH key-based authentication  on Windows & Linux
- Headless Kali Linux startup using custom PowerShell function 

![](../images/project_0.png)

---

## Issue Encountered

### 1. SSH login failed after switching to key-based authentication.

Error: Permission denied (publickey)


### Investigation
```
Initial assumptions:
- Incorrect key placement  
- Wrong file permissions  
- User or group misconfiguration  

Verified:
- Public key exists in authorized_keys  
- Permissions are correctly set  
- User configuration is valid  
```

### What works for me

[Reference](https://woshub.com/using-ssh-key-based-authentication-on-windows/)

- Commented out the Match Group administrators directive in sshd_config
- Restarted SSH service

This overrides the default key location and uses:
C:\ProgramData\ssh\authorized_keys

### 2. VboxManage failed to read kali-linux image

VBoxManage.exe: error: Could not find a registered machine named 'kali-linux'

### Investigation
```
Initial assumptions:
- Corrupt VM registration
- Command with double quote issue

Verified:
- VM exists in VBoxManage list vms, name is correct
- VBoxHeadless.exe works but blocks the terminal process to next command so I decided not to use this
```
### What works for me
- Wrap the command with cmd /c 
> ssh user@IP "cmd /c Z:\VirtualBox\VBoxManage startvm "kali-linux" --type headless"

---

### Future Updates


1. Still need to manually enter SSH password for Kali VM.
- Deploy public key to kali on 7/4/2026
> type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh kali@IP "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

---
[Home](../README.md) 