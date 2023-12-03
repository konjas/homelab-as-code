# homelab-as-code

## prerequisites

`pve_cluster_pass` variable located in `inventory/00-proxmox.yaml` needs to be filled with either plain text or encrypted root password of the `pve_cluster_starting_node`.

To generate encrypted password, follow these steps:

1. Create secrets file with some identifier and the encryption password:
```
echo 'pve: this-is-an-encryption-password' >> $HOME/.ansible/secrets.txt
```

2. Encrypt the cluster password, using the encryption password and the variable name:
```
ansible-vault encrypt_string --vault-id pve@$HOME/.ansible/secrets.txt 'my-top-secret-cluster-password' --name 'pve_cluster_pass'
```

3. The encrypted value will be prited. Paste it to the yaml file specified at the beginning.

## how to apply

Run following command and pass SSH password to configure proxmox hosts:
```
ansible-playbook run.yaml -i inventory -u root --vault-id pve@$HOME/.ansible/secrets.txt -k
```

If you're using plaintext password, just omit the `--vault-id <id>@<path>` parameter.

## what it does

Uses SSH to login as root to the proxmox hosts to:
* configure APT to use non-free Debian software
* configure reverse proxy to enable web interface on port 80
* enable power saving features
* enable PCI(e) devices passthrough to vistual machines
* install useful tools, like vim, htop or ncdu and configure them using my favourite settings
* create a PVE cluster on selected Proxmox server
* join all the other Proxmox servers to the PVE cluster
