Proxmox_VMs_Create_k3s
=========

Creating virtual machines on Proxmox for subsequent deployment of the k3s cluster

Requirements
------------

Proxmox 8.2.4+\
ansible 3.1.2+\
ansible-galaxy 2.16.11+\
Not tested on earlier versions

Role Variables
--------------

___proxmox_api_host:___ "127.0.0.1"\
___proxmox_api_user:___ "root@pam"\
___proxmox_api_password:___ "password"\
___proxmox_node:___ "pve"\
___vmid:___ 100 - ID template in proxmox

Dependencies
------------

Dependencies are absent

Example Playbook
----------------

```
# ansible-playbook -i inventory.yml playbook-VMs-create.yml
- name: Create VMs in Proxmox
  hosts: proxmox
  vars:
    proxmox_api_host: "proxmox1.home.local"
    proxmox_api_user: "root@pam"
    proxmox_api_password: "11111111"
    proxmox_node: "proxmox1"
    vm_ciuser: "murzik2142"
    vm_sshkeys: "ssh-ed25519 AAAAC rpi1-b+
          \nssh-ed25519 AAAAC srv-ansible
          \nssh-ed25519 AAAAC PC-Marat-WSL"
    vmid_template: 9001
    vm_storage: "NGFF"
    vm_network: '{"net0":"name=eth0,ip=dhcp,ip6=dhcp,bridge=vmbr0,tag=2"}'
    vm_dns: '172.25.115.53'
    vm_domain: 'home.local'
    vm_115_addr: '172.25.115.'
    vm_115_gw: "{{ vm_115_addr }}1"
    # k3s vm server vars
    vm_count_server: 3
    vm_server_name_prefix: "k3s-server-"
    vm_server_memory: 2048
    vm_server_cores: 2
    vm_server_id: 201
    vm_server_addr: 31
    vm_server_disk: 32
    # k3s vm worker vars
    vm_count_worker: 3
    vm_worker_name_prefix: "k3s-worker-"
    vm_worker_memory: 4096
    vm_worker_cores: 2
    vm_worker_id: 301
    vm_worker_addr: 41
    vm_worker_disk: 64
  roles:
    - Proxmox_VMs_Create_k3s
```

License
-------

BSD-3-Clause

Author Information
------------------

Murzabaev Marat (murzik2142@gmail.com)
