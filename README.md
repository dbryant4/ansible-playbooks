# Ansible Playbooks To Deploy Rasp Pis

## Overview

These are just a collection of Ansible playbooks that I use to help when deploying new Raspberry Pis. There are currently only 2 roles, `1wire` and `common`. `common` handles many tasks which are common on all of my Pis. `1wire` sets up the Pi to work with 1wire temperature sensors. It also downloads a Python script to `/root/` which reads the temperatures and sends the information to a grpahite server. 

## Getting started
To deploy a raspberry Pi, run the command below. After the first run, you can remove the `-k` option since the local machine's public SSH key will be set as an authorized key.

```
ansible-playbook -i hosts site.yml --extra-vars "host=192.168.101.125 hostname=devpi1 role=1wire" -k --sudo
```