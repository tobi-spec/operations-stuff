## APT

update index of accessible packages
``
sudo apt update
``

install package
``
sudo apt install <package>
``

remove package
``
sudo apt remove <package>
``

search for avaibale packages
``
sudo apt search <package>
``

upgrades only packages which doesn't need new packages/dependencies to be installed
``
sudo apt upgrade
``

upgrades all packages, even when new packages/dependencies for this have to be installed
``
sudo apt dist-upgrade
``

removes all packages which are not used as dependencies anymore
``
sudo apt autoremove
``

reboots server
``
sudo reboot
``

get list of apt sources
``
sudo cat /etc/apt/sources.list
``