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

### Installing ansible
#### On a client
I suggest you follow the official ansible instructions for installing ansible on your client. They can be found [here|https://docs.ansible.com/ansible/2.9/installation_guide/intro_installation.html].

#### Locally on your node
To install ansible on a Debian system run the following command:
```
sudo apt update & sudo apt install ansible -y
```

#### Cloning this repo
To clone this repo run:
```
```

## Support
For now I would only recommend using this repo with Debian and x64 systems.

## For newbies
* Uncomment: If the character # appears on a line the rest of the text on that line is ignored. If the documentation tells you to uncomment a line, it means you should remove the first occurence of #.

## Troubleshooting

### permission denied while trying to connect to the Docker daemon socket
If you see this error try to log out and back in. When docker is installed either by this script or rocketpool it adds your user to a group that is allowed to run docker. But it doesn't update until you log out and back in.