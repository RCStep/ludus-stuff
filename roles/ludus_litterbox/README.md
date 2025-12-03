# README

# Ansible Role: ludus_litterbox

I had made this Litterbox role, but I think professor-moody.ludus_litterbox is a better one. Just use that one instead :)

# Litterbox Red Team Sandbox toolkit installation (Windows Only)

This Ansible task automates the installation of the Littebox payload testing sandbox from https://github.com/BlackSnufkin/LitterBox.

Litterbox is placed on the taget, a python venv environment created, and an elevated startup task created for the default ludus range localuser account.

The config.yaml file is also edited to a host of 0.0.0.0 to make the web front end available externally. A firewall rule is also created on the host to expose port 1337.

Litterbox can be acessed at http://X.X.X.X:1337, where X.X.X.X is the ludus range IP of the installed host.

## Requirements

- A target Windows distribution of Windows 10 or 11.
- No MDE deployments on the host or other AV/EDR that would automatically clean/quarantine any uploaded payloads.

## Dependencies

You may opt to precompile and alter the LitterBox source files and place them in the /files directory. Rename the file to LitterBox.zip

## Notes

The RedEdr tooling included in the LitterBox dynamic analysis may still not run despite installing Visual Studio 2022 Community during LitterBox prerequisite installtions. This is a known issue.

## Example Playbook

```yaml
- hosts: {{ thing }}_hosts
  roles:
    - ludus_litterbox
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
      - ludus_litterbox
```
## Variables

defaults in defaults/main.yml

ludus_litterbox_github_url: "https://github.com/BlackSnufkin/LitterBox.git"
ludus_litterbox_install_path: "C:\\LitterBox"
ludus_litterbox_task_username: "localuser" (the default local admin account for your ludus range)
ludus_litterbox_task_password: "password" (the default local admin password for your ludus range)
ludus_litterbox_zip: "files/LitterBox.zip"
ludus_litterbox_port: 1337

## Error Handling

- The onboarding script attempts to delete processes that are already running LitterBox environments on redeployment.
- If redeployment efforts are failing, you may need to kill the powershell and python processes runing as "localuser" on the host. These processes are started on login by the Litterbox startup task.

## Usage

Include this role or task file in your playbook targeting Windows hosts. 

---
