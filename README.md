# Ansible Playbooks To Deploy Rasp Pis

## Overview

These are just a collection of Ansible playbooks that I use to help when deploying new Raspberry Pis. There are currently only 2 roles, `1wire` and `common`. `common` handles many tasks which are common on all of my Pis. `1wire` sets up the Pi to work with 1wire temperature sensors. It also downloads a Python script to `/root/` which reads the temperatures and sends the information to a grpahite server. 

## Getting started
To deploy a raspberry Pi, run the command below. After the first run, you can remove the `-k` option since the local machine's public SSH key will be set as an authorized key.

```
ansible-playbook -i hosts site.yml --extra-vars "host=192.168.101.125 hostname=devpi1 role=1wire" -k --sudo
```

## Roles
Currentlty there are three roles which are listed below.

-  1wire - sets up 1-wire temperature sensors to colelct temperature readings and send that information back to a grphite server
-  tmp102 - sets up the pi to collect data from a tmp102 temperature sensor to send back to a grpahite server
-  display - sets up a pi to start up the desktop and run chromium with a specific URL. This is designed for display boards. Also, this role installs a vnc server for easy management
-  bind - Sets up a basic bind server for the "home" domain. This also
   creates a DNSSEC key and stores it as a fact.
-  dhcpd - Sets up a basic DHCP server. If the `bind` role has been ran
   before the `dhcpd` role, and DHCP leases will automatically be pushed
   to bind.
-  tftpd - Sets up a basic tftp server for PXE booting. This includes
   setting up pxelinux.0 and a basic menu. `dhcpd` is required for this
   to work.

## Variables
-  skip_update - Skips the apt-get update call in the common role
-  hostname - if this is provide, the hostname will be set on the node

## Requirements

### route53-dyndns
- A JSON file must exist in /etc/ansible/facts.d called aws.fact. The
  file should look similar to the following and must contain proper AWS
credentials to update an A record in AWS route53.
```
{
"access_key":"AWS_ACCESS_KEY",
"secret_key":"AWS_SECRET_KEY"
}
```
