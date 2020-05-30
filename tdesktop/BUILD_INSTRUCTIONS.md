# Build Instructions for Ubuntu target

// These instructions are taken from https://github.com/nebula-chat-fork/clients/blob/master/.github/workflows/tdesktop_linux.yml with modifications from https://github.com/telegramdesktop/tdesktop/blob/dc8abc74ed4d72a73315550b91283ff1f2e44199/docs/building-cmake.md

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
zlib1g-dev yasm cmake xutils-dev bison python-xcbgen libboost-all-dev

export MAKE_THREADS_CNT=-j$(nproc)

cd Libraries

git clone https://github.com/ericniebler/range-v3
cd range-v3
git checkout a2bf5d0596dd2ffc75c2623b62d6226915609622
cd ..
git clone https://github.com/telegramdesktop/zlib.git
cd zlib
./configure
make $MAKE_THREADS_CNT
sudo make install
cd ..
git clone https://github.com/xiph/opus
cd opus
git checkout v1.2.1
./autogen.sh
./configure
make $MAKE_THREADS_CNT
sudo make install
cd ..
git clone https://github.com/01org/libva.git
cd libva
./autogen.sh --enable-static
make $MAKE_THREADS_CNT
sudo make install
cd ..
git clone git://anongit.freedesktop.org/vdpau/libvdpau
cd libvdpau
git checkout a21bf7aa438f5dd40d0a300a3167aa3d6f26dccc
./autogen.sh --enable-static
make $MAKE_THREADS_CNT
sudo make install
cd ..
git clone https://github.com/FFmpeg/FFmpeg.git ffmpeg
cd ffmpeg
git checkout release/3.4
./configure --prefix=/usr/local --disable-programs --disable-doc --disable-everything --enable-protocol=file --enable-libopus --enable-decoder=aac --enable-decoder=aac_latm --enable-decoder=aasc --enable-decoder=flac --enable-decoder=gif --enable-decoder=h264 --enable-decoder=h264_vdpau --enable-decoder=mp1 --enable-decoder=mp1float --enable-decoder=mp2 --enable-decoder=mp2float --enable-decoder=mp3 --enable-decoder=mp3adu --enable-decoder=mp3adufloat --enable-decoder=mp3float --enable-decoder=mp3on4 --enable-decoder=mp3on4float --enable-decoder=mpeg4 --enable-decoder=mpeg4_vdpau --enable-decoder=msmpeg4v2 --enable-decoder=msmpeg4v3 --enable-decoder=opus --enable-decoder=pcm_alaw --enable-decoder=pcm_alaw_at --enable-decoder=pcm_f32be --enable-decoder=pcm_f32le --enable-decoder=pcm_f64be --enable-decoder=pcm_f64le --enable-decoder=pcm_lxf --enable-decoder=pcm_mulaw --enable-decoder=pcm_mulaw_at --enable-decoder=pcm_s16be --enable-decoder=pcm_s16be_planar --enable-decoder=pcm_s16le --enable-decoder=pcm_s16le_planar --enable-decoder=pcm_s24be --enable-decoder=pcm_s24daud --enable-decoder=pcm_s24le --enable-decoder=pcm_s24le_planar --enable-decoder=pcm_s32be --enable-decoder=pcm_s32le --enable-decoder=pcm_s32le_planar --enable-decoder=pcm_s64be --enable-decoder=pcm_s64le --enable-decoder=pcm_s8 --enable-decoder=pcm_s8_planar --enable-decoder=pcm_u16be --enable-decoder=pcm_u16le --enable-decoder=pcm_u24be --enable-decoder=pcm_u24le --enable-decoder=pcm_u32be --enable-decoder=pcm_u32le --enable-decoder=pcm_u8 --enable-decoder=pcm_zork --enable-decoder=vorbis --enable-decoder=wavpack --enable-decoder=wmalossless --enable-decoder=wmapro --enable-decoder=wmav1 --enable-decoder=wmav2 --enable-decoder=wmavoice --enable-encoder=libopus --enable-hwaccel=h264_vaapi --enable-hwaccel=h264_vdpau --enable-hwaccel=mpeg4_vaapi --enable-hwaccel=mpeg4_vdpau --enable-parser=aac --enable-parser=aac_latm --enable-parser=flac --enable-parser=h264 --enable-parser=mpeg4video --enable-parser=mpegaudio --enable-parser=opus --enable-parser=vorbis --enable-demuxer=aac --enable-demuxer=flac --enable-demuxer=gif --enable-demuxer=h264 --enable-demuxer=mov --enable-demuxer=mp3 --enable-demuxer=ogg --enable-demuxer=wav --enable-muxer=ogg --enable-muxer=opus
make $MAKE_THREADS_CNT
sudo make install
cd ..
git clone https://git.assembla.com/portaudio.git
cd portaudio
git checkout 396fe4b669
./configure
make $MAKE_THREADS_CNT
sudo make install
cd ..
git clone git://repo.or.cz/openal-soft.git
cd openal-soft
git checkout openal-soft-1.19.1
cd build
if [ `uname -p` == "i686" ]; then
cmake -D LIBTYPE:STRING=STATIC -D ALSOFT_UTILS:BOOL=OFF ..
else
cmake -D LIBTYPE:STRING=STATIC ..
fi
make $MAKE_THREADS_CNT
sudo make install
cd ../..
git clone https://github.com/openssl/openssl
cd openssl
git checkout OpenSSL_1_0_1-stable
./config
make $MAKE_THREADS_CNT
sudo make install
cd ..
git clone https://github.com/xkbcommon/libxkbcommon.git
cd libxkbcommon
git checkout 293c704cbedd95779351a7295683159e93e12de7
./autogen.sh --disable-x11
make $MAKE_THREADS_CNT
sudo make install
cd ..
git clone git://code.qt.io/qt/qt5.git qt5_6_2
cd qt5_6_2
perl init-repository --module-subset=qtbase,qtimageformats
git checkout v5.6.2
cd qtimageformats && git checkout v5.6.2 && cd ..
cd qtbase && git checkout v5.6.2 && cd ..
cd qtbase && git apply ../../../tdesktop/Telegram/Patches/qtbase_5_6_2.diff && cd ..
cd qtbase/src/plugins/platforminputcontexts
git clone https://github.com/telegramdesktop/fcitx.git
git clone https://github.com/telegramdesktop/hime.git
cd ../../../..
./configure -prefix "/usr/local/tdesktop/Qt-5.6.2" -release -force-debug-info -opensource -confirm-license -qt-zlib -qt-libpng -qt-libjpeg -qt-freetype -qt-harfbuzz -qt-pcre -qt-xcb -qt-xkbcommon-x11 -no-opengl -no-gtkstyle -static -openssl-linked -nomake examples -nomake tests
make $MAKE_THREADS_CNT
sudo make install
cd ..
git clone https://chromium.googlesource.com/external/gyp
cd gyp
git checkout 702ac58e47
git apply ../../tdesktop/Telegram/Patches/gyp.diff
cd ..

git clone https://chromium.googlesource.com/breakpad/breakpad
cd breakpad
git checkout bc8fb886
git clone https://chromium.googlesource.com/linux-syscall-support src/third_party/lss
cd src/third_party/lss
git checkout a91633d1
cd ../../..
cd ~/git/Libraries/breakpad/
./configure
make $MAKE_THREADS_CNT
sudo make install

cd src
rm -r testing
git clone https://github.com/google/googletest testing
cd tools
echo "old tools.gyp: [`cat tools.gyp`]"
# sed -i "s/gypi...$/gypi'],'cxxflags':['-std=c++11'],/" tools.gyp 
sed -i 's/minidump_upload.m/minidump_upload.cc/' linux/tools_linux.gypi
echo "new tools.gyp: [`cat tools.gyp`]"

../../../gyp/gyp  --depth=. --generator-output=.. -Goutput_dir=../out tools.gyp --format=cmake
cd ../../out/Default
```

Then, patch `CMakeLists.txt` (insert line `set(CMAKE_CXX_FLAGS '-std=c++11')`) as:

```
cmake_minimum_required(VERSION 2.8.8 FATAL_ERROR)
cmake_policy(VERSION 2.8.8)
project(common_unittests)
set(configuration "Default")
enable_language(ASM)
set(builddir "${CMAKE_CURRENT_BINARY_DIR}")
set(obj "${builddir}/obj")

set(CMAKE_C_OUTPUT_EXTENSION_REPLACE 1)
set(CMAKE_CXX_OUTPUT_EXTENSION_REPLACE 1)

set(CMAKE_NINJA_FORCE_RESPONSE_FILE 1)

set(CMAKE_CXX_FLAGS '-std=c++11')
```

Then,

```
echo "gcc --version: `gcc --version|head -1`"
cmake .
make $MAKE_THREADS_CNT dump_syms
cd ../../..
```

Then, patch and build:

```
cd ~/git/

git clone --recursive https://github.com/nebula-chat-fork-originals/tdesktop.git 
cd tdesktop
git checkout dc8abc74ed4d72a73315550b91283ff1f2e44199
git reset --hard
cd ..

cd tdesktop

git submodule init
git submodule sync
git submodule update

echo "patching"

git apply ~/git/i2pgram-clients/tdesktop/config.h.diff
git apply ~/git/i2pgram-clients/tdesktop/dc_options.cpp.diff
git apply ~/git/i2pgram-clients/tdesktop/launcher_linux.cpp.diff
git apply ~/git/i2pgram-clients/tdesktop/launcher_mac.mm.diff
git apply ~/git/i2pgram-clients/tdesktop/launcher_win.cpp.diff
git apply ~/git/i2pgram-clients/tdesktop/telegram_mac.gypi.diff
git apply ~/git/i2pgram-clients/tdesktop/update_checker.cpp.diff

echo "patched"

cd ~/git/tdesktop/Telegram

# test credentials specified at tdesktop/Telegram/gyp/generate.py
# Test credentials are documented with:
# "Your users will start getting internal server errors on login
# if you deploy an app using those 'api_id' and 'api_hash'."
gyp/refresh.sh --api-id 17349 --api-hash 344583e45741c457fe1862106095a5eb

export HomePath=~/git

echo "building tdesktop"
cd $HomePath/tdesktop/out/Debug
make $MAKE_THREADS_CNT
            
```

TBD

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test -y && \
sudo apt-get update && \
sudo apt-get install gcc-8 g++-8 -y && \
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 60 && \
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-8 60 && \
sudo update-alternatives --config gcc && \
sudo add-apt-repository --remove ppa:ubuntu-toolchain-r/test -y

# pwd
/home/user/git/Libraries/range-v3
# git checkout 4d6a463bca51bc316f9b565edd94e82388206093
```
