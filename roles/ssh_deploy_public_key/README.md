# Deploy your ssh key to the node
This role is part 1 of the section [ESSENTIAL: Secure your SSH Access|https://docs.rocketpool.net/guides/node/securing-your-node#essential-secure-your-ssh-access], [Adding the Public Key to your Node|https://docs.rocketpool.net/guides/node/securing-your-node#adding-the-public-key-to-your-node]. Part 2 is performed in ssh_allow_only_key_access.

It is worth noting that by default this role removes all existing public keys on the node. The role also supports deploying two public keys, a primary and a backup.

## Prerequisites
For this role to be executed you must define the ssh_public_key variable in the hosts.yml file. The generation of the ssh public key file is out of scope of this tool, but it is explained in the rocketpool docs.

