FROM opensuse/leap:15.0

RUN zypper ar  -G  -C -p 80 http://download.opensuse.org/repositories/devel:/languages:/go/openSUSE_Leap_15.0/ golang

RUN zypper in -y -f --replacefiles --force-resolution --no-recommends \
    libgcrypt-devel  make cmake  gcc-c++   \
    libQt5Core-devel  zlib-devel libQt5Network-devel libqt5-qttools-devel libqt5-linguist-devel \
    libQt5Concurrent-devel libQt5Widgets-devel libQt5DBus-devel  argon2-devel libQt5Test-devel \
    libQt5X11Extras5 libqt5-qtx11extras-devel \
    acl autoconf dnsmasq dnsmasq-utils git go libacl-devel \
    libcap-devel liblxc1 liblxc-devel libtool libuv-devel \
    make pkg-config rsync squashfs tar tcl xz-devel libapparmor-devel libseccomp-devel \
    lvm2 thin-provisioning-tools btrfsprogs curl gettext-runtime gettext-tools jq sqlite3  bzr uuidd
    

