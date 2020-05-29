# Build Instructions for Ubuntu target

// these instructions are taken from https://github.com/nebula-chat-fork/clients/blob/master/.github/workflows/tdesktop_linux.yml

1. install ubuntu 14.04 into virtualbox vm with 300GB storage on disk

TBD

sudo bash

cfgFile="/etc/dpkg/dpkg.cfg.d/no_man"
sudo touch $cfgFile
p() {
  sudo echo "path-exclude=/usr/share/$1/*" >> $cfgFile
}
p man
p locale
p doc

TBD
