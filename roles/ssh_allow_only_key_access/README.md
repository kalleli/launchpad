# Deploy your ssh key to the node
This role is part 2 of the section [ESSENTIAL: Secure your SSH Access|https://docs.rocketpool.net/guides/node/securing-your-node#essential-secure-your-ssh-access], [Disable Login-via-Password|https://docs.rocketpool.net/guides/node/securing-your-node#disable-login-via-password]. Part 1 is performed in ssh_deploy_public_key.

## Prerequisites
For this role to be executed you must define the ssh_public_key variable in the hosts.yml file. The generation of the ssh public key file is out of scope of this tool, but it is explained in the rocketpool docs. This is to make sure that you don't lock yourself out of the node.
