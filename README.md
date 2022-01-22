# Ansible — JetBrains Projector

This playbook installs [JetBrains Projector](https://lp.jetbrains.com/projector/) on a Debian/Ubuntu instance.

**Assumption:** Instance deployed using the Terraform script below,
* terraform__oci-instance-3
	* GitHub: [github.com/k3karthic/terraform__oci-instance-3](https://github.com/k3karthic/terraform__oci-instance-3)
	* Codeberg: [codeberg.org/k3karthic/terraform__oci-instance-3](https://codeberg.org/k3karthic/terraform__oci-instance-3)

## Code Mirrors

* GitHub: [github.com/k3karthic/ansible__jetbrains-projector](https://github.com/k3karthic/ansible__jetbrains-projector/)
* Codeberg: [codeberg.org/k3karthic/ansible__jetbrains-projector](https://codeberg.org/k3karthic/ansible__jetbrains-projector)

## Requirements

Install the following before running the playbook,
```
pip install oci
ansible-galaxy collection install oracle.oci
```

## Dynamic Inventory

The Oracle [Ansible Inventory Plugin](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/ansibleinventoryintro.htm) populates public Ubuntu instances.

All target Ubuntu instances must have the freeform tag `jetbrains_projector: yes`.

## Configuration

1. Update `inventory/oracle.oci.yml`,
    1. Specify the region where you have deployed your server on Oracle Cloud. List of regions are at [docs.oracle.com/en-us/iaas/Content/General/Concepts/regions.htm](https://docs.oracle.com/en-us/iaas/Content/General/Concepts/regions.htm).
    1. Configure the authentication as per the [Oracle Guide](https://docs.oracle.com/en-us/iaas/Content/API/Concepts/sdkconfig.htm#SDK_and_CLI_Configuration_File)
1. Set username and ssh authentication in `inventory/group_vars/all.yml`

## Deployment

Run the playbook using the following command,
```
./bin/apply.sh
```

## Encryption

Encrypt sensitive files (SSH private keys) before saving them. `.gitignore` must contain the unencrypted file paths.

Use the following command to decrypt the files after cloning the repository,

```
$ ./bin/decrypt.sh
```

Use the following command after running terraform to update the encrypted files,

```
$ ./bin/encrypt.sh <gpg key id>
```
