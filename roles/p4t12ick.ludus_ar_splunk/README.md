# Ansible Role: ([Ludus](https://ludus.cloud)) Attack Range Splunk

An Ansible Role that installs Splunk on Ubuntu 22.04 and configure it with common Splunk apps. 
This will install and configure Splunk similar to the Splunk server in [Attack Range](https://github.com/splunk/attack_range)

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):
```
ludus_splunk_url: https://download.splunk.com/products/splunk/releases/9.3.0/linux/splunk-9.3.0-51ccf43db5bd-Linux-x86_64.tgz
ludus_splunk_password: changeme123!
ludus_splunk_apps:
    - splunk-add-on-for-microsoft-windows_901.tgz
    - splunk-add-on-for-sysmon-for-linux_100.tgz
    - splunk-add-on-for-sysmon_402.tgz
    - splunk-add-on-for-unix-and-linux_1000.tgz
    - splunk-common-information-model-(cim)_602.tgz
    - DA-ESS-ContentUpdate-latest.tar.gz
ludus_splunk_s3_bucket_url: https://attack-range-appbinaries.s3-us-west-2.amazonaws.com
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: attack_range_splunk
  roles:
    - P4T12ICK.ludus_ar_splunk
```

## Example Ludus Range Config

```yaml
ludus:
  - vm_name: "{{ range_id }}-ar-splunk"
    hostname: "{{ range_id }}-ar-splunk"
    template: ubuntu-22.04-x64-server-template
    vlan: 20
    ip_last_octet: 1
    ram_gb: 16
    cpus: 8
    linux: true
    roles:
      - P4T12ICK.ludus_ar_splunk
```

## License
Apache License 2.0

## Author Information
This role was created by [P4T12ICK](https://github.com/P4T12ICK), for [Ludus](https://ludus.cloud/).
