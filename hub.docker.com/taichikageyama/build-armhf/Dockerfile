FROM debian:stable
LABEL maintainer="32001477+TaichiKageyama@users.noreply.github.com"
RUN     set -ex;                                                          \
        apt-get -qq update;                                               \
        DEBIAN_FRONTEND=noninteractive apt-get -qq                        \
            -o Dpkg::Options::="--force-confdef"                          \
            -o Dpkg::Options::="--force-confold" install -y               \
    git bc openssl build-essential crossbuild-essential-armhf python      \
    autotools-dev autoconf automake libssl-dev device-tree-compiler       \
    git-core dosfstools mtools libpython-dev parted gdisk ncurses-dev     \
    kmod ccache swig libpython-dev;                                       \
    apt-get -qq autoclean -y;                                             \
    apt-get -qq clean -y;                                                 \
    rm -rf /var/lib/apt/lists/*;

