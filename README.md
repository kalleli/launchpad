# Launchpad
Launchpad is a tool for automating the preparation and securing of you rocketpool or nodeset node. It aims to automate everything between finishing the OS installation and [installing the smartnode stack|https://docs.rocketpool.net/guides/node/docker#installing-the-smartnode-stack].

Launchpad can be used both directly on the node or remotely from the client you use to manage your node. It connects to the node using ssh.

## Prerequisites
Before starting you need to have completed a fresh install of one of the supported operating systems, either on your own hardware or a vps. If you plan to run launchpad remotely you need to have selected to install the ssh server in the OS installation steps.

Launchpad uses a tool called ansible to set up your node. If you are using a windows computer as a client you need Windows Subsystem for Linux (WSL) since ansible can't be installed on windows. If you don't have or want WSL I suggest you run launchpad directly on your node.

## How to run launchpad
Running launchapd has four steps
* Installing ansible on your remote client or directly on your node
* Cloning this repository
* Editing the hosts.yml file to match your setup and needs
* Running either the rocketpool or nodeset playbook depending on what protocol you are going to run

### tldr
Run these commands locally on your debian node.

#### Prerequirements
```
sudo apt update && sudo apt install ansible-core git -y
git clone https://github.com/kalleli/launchpad.git && cd launchpad
```
#### Rocketpool
```
ansible-playbook setup_rocketpool_node.yml -i hosts.yml --ask-become
```
#### NodeSet
```
ansible-playbook setup_nodeset_node.yml -i hosts.yml --ask-become
```
#### NodeSet beta
```
ansible-playbook setup_nodeset_beta_node.yml -i hosts.yml --ask-become
```

### Installing ansible
#### On a client
I suggest you follow the official ansible instructions for installing ansible on your client. They can be found [here|https://docs.ansible.com/ansible/2.9/installation_guide/intro_installation.html].

#### Locally on your node
To install ansible on a Debian system run the following command:
```
sudo apt update & sudo apt install ansible -y
```

### Cloning this repo
To clone this repository we need git installed. Some installations will have it by default but if yours is missing it run:
```
sudo apt update & sudo apt install git -y
```
We can then clone this repo by running. The files will be placed in a sub folder, launchpad.
```
git clone https://github.com/kalleli/launchpad.git
```

### Editing the hosts.yml file
Have a look at the hosts.yml file and see what kind of options are available.

#### If you are running locally on the node
You could in theory skip this step. The default hosts.yml file is made for you. But you might want to look at the options regardless to see if you want or need some of the optional things (like opening the QUICK port if you choose to run lighthouse).

#### If you are running remotely from a client
The mandatory thing here is to set the ip of your node, replace localhost with an ip adress.

I highly recommend you set the ssh public key variable, this will trigger launchpad to deploy the key and lock down your node so that password authentication is no longer allowed.

An example hosts.yml file could look like this:
```
---
rocketpool-node:
  hosts:
    192.168.0.33: # replaced localhost with the ip of your node
      ssh_public_key: ~/.ssh/id_rsa.pub
      firewall_execution_client_port: 30303
      firewall_consensus_client_port: 9001
```

### Running one of the playbooks
Strap in, it's time for liftoff. The last step is to run either the rocketpool or the nodeset playbook depending on what protocol you plan to run.

Ansible will ask you for the BECOME password. It's ansibles way of asking you for the sudo password on your node.

#### Rocketpool
Simply run the following:
´´´
ansible-playbook setup_rocketpool_node.yml -i hosts.yml --ask-become
´´´
If its the first time you ssh into the node it will ask you to confirm the fingerprint, simply answer yes.

#### NodeSet
Run the following:
´´´
ansible-playbook setup_nodeset_node.yml -i hosts.yml --ask-become
´´´
If its the first time you ssh into the node it will ask you to confirm the fingerprint, simply answer yes.

## Support
For now I would only recommend using this repo with Debian and x64 systems.

## For newbies
* Uncomment: If the character # appears on a line the rest of the text on that line is ignored. If the documentation tells you to uncomment a line, it means you should remove the first occurence of #.

## Troubleshooting

### permission denied while trying to connect to the Docker daemon socket
If you see this error try to log out and back in. When docker is installed either by this script or rocketpool it adds your user to a group that is allowed to run docker. But it doesn't update until you log out and back in.