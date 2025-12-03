# README

# Ansible Role: ludus_mde_agent

# Microsoft Defender for Endpoint (MDE) Agent Installation and Onboarding (Windows Only)

This Ansible task automates the installation and onboarding of the Microsoft Defender for Endpoint (MDE) agent on supported Windows operating systems.

## Requirements

An active Microsoft Defender for Endpoint (MDE) subsciption.

A target Windows distribution of Windows 10, 11, 2012R2, 2016, 2019, 2022, or 2025.

## Dependencies

Generation and renaming of the appropriate installer scripts and packages from the MDE security portal. These file are palced in the "files" folder.

## Example Playbook

```yaml
- hosts: {{ thing }}_hosts
  roles:
    - ludus_mde_agent
```

## Example Ludus Range Config

```yaml
ludus:
  - vm_name: "{{ range_id }}-ad-win11-23h2-enterprise-x64-1"
    hostname: "{{ range_id }}-WIN11-23H2-1"
    template: win11-23h2-x64-enterprise-template
    vlan: 10
    ip_last_octet: 21
    ram_gb: 4
    cpus: 2
    windows:
      install_additional_tools: false
    domain:
      fqdn: ludus.domain
      role: member
    roles:
      - ludus_mde_agent
```
## Overview

- **Purpose:**  
  Installs and onboards the MDE agent on Windows hosts, selecting the correct onboarding package based on the OS version, and verifies successful installation.

- **Scope:**  
  This playbook runs **only** on Windows hosts (`ansible_os_family == "Windows"`).

## Steps Performed

1. **Display OS Details:**  
   Outputs the OS family, major version, and full version for troubleshooting and logging.

2. **Select Onboarding Package:**  
   Sets the correct onboarding package (`mde_zip`) based on the detected Windows version.

3. **Prepare Working Directory:**  
   Ensures `C:\Temp` exists and copies the onboarding package zip file to this directory.

4. **Unzip and Install:**  
   - Unzips the onboarding package in `C:\Temp`.
   - Runs the onboarding script, with retries for robustness.
   - Output log for the installation script is written to the host in `C:\Temp\mde_onboarding.log`.

5. **Verify Installation:**  
   - Checks if the MDE agent process (`MsSense`) is running.
   - Prints the result of the agent check for visibility.

## Variables

- `ansible_os_family`: Used to ensure tasks run only on Windows.
- `ansible_distribution_version`: Used to select the correct onboarding package.

The targeted OS versions for onboarding are specific Windows builds, as defined in the README.md found in the files folder. The playbook supports:

- **Windows 10/11** (builds: 
`10.0.19045.0`,  # Windows 10 22H2
`10.0.22621.0`,  # Windows 11 22H2
`10.0.22631.0`,  # Windows 11 23H2
`10.0.26100.0`,  # Windows 11 24H2 (also the same build number for Windows 2025 Server)
`10.0.26200.0`)  # Windows 11 25H2 

  - Uses: `Win10_11_GatewayWindowsDefenderATPOnboardingPackage.zip`
- **Windows Server 2019/2022** (builds: 
`10.0.17763.0`,  # Windows 2019 Server
`10.0.20348.0`)  # Windows 2022 Server
  - Uses: `Win2019_2022_2025_GatewayWindowsDefenderATPOnboardingPackage.zip`

The playbook will only proceed if the detected `ansible_distribution_version` matches one of these values.

## Error Handling

- The onboarding script and agent check steps include retries and error handling to ensure reliability.

## Usage

Include this role or task file in your playbook targeting Windows hosts. Ensure the onboarding package files are present in the specified `files/` directory.

---

**Note:**  
This playbook is intended for use in environments where Microsoft Defender for Endpoint (MDE) onboarding is required for Windows systems. Adjust the onboarding package versions and paths as needed for your environment.