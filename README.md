# homelab-as-code

## how to apply

run following command and pass SSH password to configure proxmox hosts:
```
ansible-playbook prepare-ansible-target.yaml -i inventory -k
```

## what it does

Uses SSH to login as root to the proxmox hosts to:
* configure APT to use non-free Debian software
* configure reverse proxy to enable web interface on port 80
* enable power saving features
* enable PCI(e) devices passthrough to vistual machines
* install useful tools, like vim, htop or ncdu and configure them using my favourite settings

