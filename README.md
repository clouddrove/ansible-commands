<p align="center"><img src="https://i.imgur.com/nvYD94K.png" /></p>

> Kubernetes commands

<p align="center">
    <a href="LICENSE.md">
      <img src="https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square" alt="Software License">
    </a>
    <a href="https://www.paypal.me/anmolnagpal">
      <img src="https://img.shields.io/badge/PayPal-Buy%20Me%20A%20BEER-blue.svg?style=flat-squares" alt="Donate">
    </a>
  </p>
</p>

Helper setup to edit .yaml files with Vim:

- [VIM Setup for Yaml files](#vim-setup-for-yaml-files)

List of general purpose commands for Kubernetes management:

- [Installation](#installation)
- [Inventory/Hosts](#inventory)
- [Check Connection](#check-connection)
- [POD Upgrade / History](#pod-upgrade-and-history)
- [Services](#services)
- [Volumes](#volumes)
- [Secrets](#secrets)
- [ConfigMaps](#configmaps)
- [Ingress](#ingress)
- [Horizontal Pod Autoscalers](#horizontal-pod-autoscalers)
- [Scheduler](#scheduler)
- [Taints and Tolerations](#tains_and_tolerations)
- [Troubleshooting](#troubleshooting)
- [Role Based Access Control (RBAC)](#role_based_access_control)
- [Security Contexts](#security_contexts)
- [Pod Security Policies](#pod_security_policies)
- [Network Policies](#network_policies)


## Installation

```
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible
$ ansible -version
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

```yamlex
$ ansible -m ping <host>
```

## Ad-Hoc Commands

#### Parallelism Shell Commands

```bash
$ ssh-agnet bash $ ssh-add ~/.ssh/id_rsa
```
> Reboot remove server using anisble
```yamlex
$ ansible mysql -a "/sbin/reboot" -f 20
```
> Run ansible using specific user
```yamlex
$ ansible nginx -a "/usr/bin/foo" -u anmolnagpal
```   
> Run ansible using specific user
```yamlex
$ ansible nginx -a "/usr/bin/foo" -u anmolnagpal
```   
#### File Transfer

> Transfer file to many servers
```yamlex
$ ansible nginx -m copy -a "src=/etc/anmol.txt dest=/tmp/anmol.txt"
```
> Transfer file with specific ownership & permission
```yamlex
$  ansible nginx -m file -a "src=/etc/anmol.txt dest=/tmp/anmol.txt mode=600"
$  ansible nginx -m file -a "src=/etc/anmol.txt dest=/tmp/anmol.txt mode=600 owner=anmol gorup=anmol"
```
> Create Directories 

```yamlex
$ ansible nginx -m file -a "dest=/tmp/clouddrove mode=755 owner=anmol gorup=anmol stage=directory"
```

> Delete Directories
```yamlex
$ ansible nginx -m file -a "dest=/tmp/clouddrove state=absent"
```

## Manage Packages



```
```

## Manage Services

```
```


More about Ansible: 

- 

## 👬 Contribution
- Open pull request with improvements
- Discuss ideas in issues

- Reach out with any feedback [![Twitter URL](https://img.shields.io/twitter/url/https/twitter.com/anmol_nagpal.svg?style=social&label=Follow%20%40anmol_nagpal)](https://twitter.com/anmol_nagpal)
