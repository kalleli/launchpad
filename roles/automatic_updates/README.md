This role automatically performs the steps from the section [ESSENTIAL: Enable Automatic Security Updates|https://docs.rocketpool.net/guides/node/securing-your-node#essential-enable-automatic-security-updates]

The automatic updates settings are deployed as two files to /etc/apt/apt.conf.d/. The reason we split the settings into two files is because the APT::Periodic settings belong in the file 20auto-updates (the file mentioned in the rpl documentation). But the Unattended-Upgrade:: settings belong in another file 52unattended-upgrades-local. The reason is that unattended-upgrades has its default settings in 50unattended-upgrades and for our settings to take higher priority we need the file to have a higher number.

The config files deployed can be found in the templates folder.

Here is the [source|https://wiki.debian.org/UnattendedUpgrades] for how to manage the config files.