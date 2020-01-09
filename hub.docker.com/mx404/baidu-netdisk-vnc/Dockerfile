FROM dorowu/ubuntu-desktop-lxde-vnc:bionic-lxqt

RUN cd /tmp; \
    curl -O https://issuecdn.baidupcs.com/issue/netdisk/LinuxGuanjia/baidunetdisk_linux_2.0.1.deb; \
    [ -f baidunetdisk_linux_2.0.1.deb ] || exit 1; \
    dpkg -i baidunetdisk_linux_2.0.1.deb; \
    rm baidunetdisk_linux_2.0.1.deb
