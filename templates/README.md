# Ludus Templates

These directories are self-contained Ludus templates.

For more information see: https://docs.ludus.cloud/docs/templates


After cloning, you may import a template with:
```
cd templates
ludus templates add -d ./ludus_template_directory --force
```

## Install pre-reqs and add all templates to Ludus

```
for DIR in $(ls .); do if [[ "$DIR" == "manual-setup-required" || "$DIR" == "README.md" ]]; then continue; else echo "Adding $DIR" && ludus templates add -d $DIR; fi; done
```

Then build any templates you wish after importing:
```
ludus templates list
ludus templates build -n ludus_template_name
```

Templates:

| Template | Description |
| ---      | ---      |
| win11-24h2-x64-enterprise-tpm | Ludus template with cpu changed to x86-64-v3 for nexted proxmox performance issues. Redueced CPU instructions mean not all 24h2+ virtualizated security protections will be enabled |
| win2025-server-x64-tpm | Ludus template with cpu changed to x86-64-v3 for nested proxmox performance issues. Redueced CPU instructions mean not all 2025+ virtualizated security protections will be enabled |

## Post Template Creation Edits ###

After creation, you may need to move the TPM State volume and change it to a qcow2 format, depending on your storage solution for the Ludus range.

Not all storage (Directory\NFS) supports taking snapshots of the default TPM State raw disk image.

This option (added in Proxmox 9.1+) allows snapshotting of Windows TPM VMs in more storage situations.

For more information on Ludus storage considerations: https://docs.ludus.cloud/docs/storage