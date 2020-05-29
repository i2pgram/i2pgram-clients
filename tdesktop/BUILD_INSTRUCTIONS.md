# Build Instructions for Ubuntu target

// These instructions are taken from https://github.com/nebula-chat-fork/clients/blob/master/.github/workflows/tdesktop_linux.yml

1. Install Ubuntu 14.04 into virtualbox vm with 300GB storage on disk
2. In a terminal,

```
$ sudo apt-get install git
$ ssh-keygen -C i2gram_build_vm_github_key
Generating public/private rsa key pair.
Enter file in which to save the key (/home/user/.ssh/id_rsa): /home/user/.ssh/i2gram_build_vm_github_key
$ cat ~/.ssh/i2gram_build_vm_github_key.pub
ssh-rsa ... i2gram_build_vm_github_key
```

3. Paste the public key into GitHub's https://github.com/settings/ssh/new with the title i2pgram_build_vm_github_key.
4. In a terminal,

```
$ cd && mkdir git && cd git
$ git clone git@github.com:i2pgram/i2pgram-clients.git
$ sudo bash

cfgFile="/etc/dpkg/dpkg.cfg.d/no_man"
sudo touch $cfgFile
p() {
  sudo echo "path-exclude=/usr/share/$1/*" >> $cfgFile
}
p man
p locale
p doc

mkdir -pv Libraries

sudo apt-get install -y software-properties-common aptitude
sudo add-apt-repository -y ppa:ubuntu-toolchain-r/test
sudo add-apt-repository -y ppa:george-edison55/cmake-3.x
sudo apt-get update
sudo apt-get install -y gcc-7 g++-7 cmake
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 60
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 60
sudo add-apt-repository --remove ppa:ubuntu-toolchain-r/test
sudo add-apt-repository --remove ppa:george-edison55/cmake-3.x
sudo aptitude install -y git libexif-dev liblzma-dev libz-dev libssl-dev libappindicator-dev \
libunity-dev libicu-dev libdee-dev libdrm-dev dh-autoreconf autoconf automake build-essential \
libass-dev libfreetype6-dev libgpac-dev libsdl1.2-dev libtheora-dev libtool libva-dev libvdpau-dev \
libvorbis-dev libxcb1-dev libxcb-image0-dev libxcb-shm0-dev libxcb-xfixes0-dev libxcb-keysyms1-dev \
libxcb-icccm4-dev libxcb-render-util0-dev libxcb-util0-dev libxrender-dev libasound-dev libpulse-dev \
libxcb-sync0-dev libxcb-randr0-dev libx11-xcb-dev libffi-dev libncurses5-dev pkg-config texi2html \
zlib1g-dev yasm cmake xutils-dev bison python-xcbgen
```

TBD
