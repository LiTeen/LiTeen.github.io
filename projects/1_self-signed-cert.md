# Secure Script Execution with Self-Signed Certificate

### Context

PowerShell blocked local script execution due to execution policy restrictions.

A common workaround is:

```powershell.exe -ExecutionPolicy Bypass -File script.ps1```

### My Approach

Used code signing with a self-signed certificate to allow script execution while keeping execution policy enforcement in place.

See [here](https://github.com/LiTeen/3ppl_fund_manager/issues/1) for implementation details.

This was less about getting the script to run, and more about understanding how trust is enforced during execution.






---
[Home](../README.md) 