<p align="center"><img src="https://i.imgur.com/xYb2PRb.png" /></p>

> Ansible commands

<p align="center">
    <a href="LICENSE.md">
      <img src="https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square" alt="Software License">
    </a>
</p>

List of general purpose commands for Ansible management:

## Installation

```bash
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
ansible --version
```

## Inventory

Example of Inventory file

```ini
[mysql]
10.0.0.13 = Env=live EcType=mysql EcName=live-mysql-0-b Az=a Nr=0
[nginx]
10.0.0.17 = Env=live EcType=nginx EcName=live-nginx-0-b Az=a Nr=0

[live:children]
mysql
nginx
```

## Check Connection

```yaml
$ ansible -m ping <host>
```

## Ad-Hoc Commands

#### Parallelism Shell Commands

```bash
ssh-agnet bash $ ssh-add ~/.ssh/id_rsa
```
> Reboot remove server using anisble
```yaml
ansible mysql -a "/sbin/reboot" -f 20
```
> Run ansible using specific user
```yaml
ansible nginx -a "/usr/bin/foo" -u anmolnagpal
```
> Run ansible using specific user
```yaml
ansible nginx -a "/usr/bin/foo" -u anmolnagpal
```
#### File Transfer

> Transfer file to many servers
```yaml
ansible nginx -m copy -a "src=/etc/anmol.txt dest=/tmp/anmol.txt"
```
> Transfer file with specific ownership & permission
```yaml
ansible nginx -m file -a "src=/etc/anmol.txt dest=/tmp/anmol.txt mode=600"
ansible nginx -m file -a "src=/etc/anmol.txt dest=/tmp/anmol.txt mode=600 owner=anmol gorup=anmol"
```
> Create Directories
```yaml
ansible nginx -m file -a "dest=/tmp/clouddrove mode=755 owner=anmol gorup=anmol stage=directory"
```
> Delete Directories
```yaml
ansible nginx -m file -a "dest=/tmp/clouddrove state=absent"
```

#### Manage Packages

> Ensure package is installed, but doesn't get updated
```yaml
ansible mysql -m apt -a "name=python state=present"
```
> Ensure package is installed to a specific version
```yaml
ansible mysql -m apt -a "name=python-2.6 state=present"
```
> Ensure package is installed with latest version
```yaml
ansible mysql -m apt -a "name=python state=latest"
```
> Ensure package is installed is not installed
```yaml
ansible mysql -m apt -a "name=python state=absent"
```

#### Manage Services

> Ensure a service is started on all nginx servers
```yaml
ansible nginx -m service -a "name=nginx state=started"
```
> Restart service on all nginx servers
```yaml
ansible nginx -m service -a "name=nginx state=restarted"
```
> Ensure a service is stopped
```yaml
ansible nginx -m service -a "name=nginx state=stopped"
```

## Playbooks

#### Playbook: Update system (Debian based)

```yaml
- hosts: local
  tasks:
    - name: Update system
      apt:
        update_cache: yes
        upgrade: yes
    - name: Remove dependencies
      apt:
        autoremove: yes
    - name: Remove useless packages from the cache
      apt:
        autoclean: yes
```

#### Sample Playbooks

```yaml
- name: dpkg --configure -a
  shell: dpkg --configure -a
  tags:
    - dpkg

- name: install system pakcages and utils
  apt:
    name: "{{ item }}"
    state: latest
    update_cache: yes
    cache_valid_time: 5400
    allow_unauthenticated: yes
  with_items:
   - ntp
   - git
   - git-core
   - htop
   - vim
   - curl
   - unzip
   - jq
   - python-setuptools
   - python-dev
   - build-essential
  tags:
    - packages
```

#### Writing Playbooks
> Create a playbook
```yaml
- hosts: live-node-01
  become: true
  roles:
    - { role: common,    tags: [ 'common'    ] }
    - { role: docker,    tags: [ 'docker'    ] }
    - { role: jenkins,   tags: [ 'agent'     ] }
    - { role: selenoid,  tags: [ 'selenoid'  ] }
```

#### Ansible Vault
> Using the argument “ — ask-vault-pass”
```
ansible-playbook users.yml --ask-vault-pass
```
> Using the argument “ — vault-password-file”
```
ansible-playbook users.yml --vault-password-file /anmol/.ansible/vault-passwd
```

More about Ansible:

- https://docs.ansible.com/ansible/latest/index.html
- https://medium.com/clouddrove/about-ansible-vault-cbeeae7add87
- https://medium.com/tech-tajawal/ansible-an-effective-it-automation-tool-be603417ea1a

## 👬 Contribution
- Open pull request with improvements
- Discuss ideas in issues

- Reach out with any feedback [![Twitter URL](https://img.shields.io/twitter/url/https/twitter.com/anmol_nagpal.svg?style=social&label=Follow%20%40anmol_nagpal)](https://twitter.com/anmol_nagpal)
