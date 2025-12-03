# Ludus Roles

These directories are self-contained Ludus roles.

For more information see: https://docs.ludus.cloud/docs/roles

After cloning, you may import a role with:
```
cd roles
ludus ansible role add -d ./ludus_role_directory
```

Roles:

| Role | Description |
| ---      | ---      |
| badsectorlabs.ludus_elastic_agent | Elastic agent role with some deployment fixes |
| ludus_litterbox | Deploys and serves the Litterbox Red Team malware sandbox |
| ludus_mde_agent | Microsoft Defender for Endpoint (MDE/ATP) Windows agent enrollment |
| p4t12ick.ludus_ar_linux | Fixes SplunkUF redeployment issues and service stop after install |
| p4t12ick.ludus_ar_splunk | Fixes splunk redeployment issues |
| p4t12ick.ludus_ar_windows | alternate choco nexus deployment, Vulnerable-AD option, SplunkUF service stop fixes, ATR install disabled |
