#
# Docker image for running snapcraft on systems where snapcraft is not available.
#

FROM ubuntu:latest

MAINTAINER Lars Boegild Thomsen <lth@cow.dk>

COPY	locale.gen /etc

RUN     export DEBIAN_FRONTEND=noninteractive && \
        apt-get -y update && \
        apt-get -y dist-upgrade && \
        apt-get -y install locales software-properties-common less vim curl git sudo snapcraft apparmor autoconf automake autopoint autotools-dev binutils build-essential bzip2 bzr comerr-dev cpp cpp-5 dbus dirmngr dpkg-dev e2fslibs-dev fakeroot g++ g++-5 gcc gcc-5 gir1.2-glib-2.0 gnupg-agent gnupg2 javascript-common libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl libapparmor-perl libasan2 libassuan0 libatomic1 libblkid-dev libc-dev-bin libc6-dev libcap-dev libcap-ng0 libcc1-0 libcgmanager-dev libcgmanager0 libcilkrts5 libdbus-1-3 libdbus-1-dev libdbus-glib-1-2 libdpkg-perl libfakeroot libfile-fcntllock-perl libfuse2 libgcc-5-dev libgirepository-1.0-1 libglib2.0-0 libglib2.0-data libgomp1 libgpgme11 libisl15 libitm1 libjs-jquery libksba8 liblsan0 libltdl-dev libltdl7 liblxc1 liblzo2-dev libmpc3 libmpfr4 libmpx0 libnet1 libnet1-dev libnih-dbus-dev libnih-dbus1 libnih-dev libnih1 libnl-3-200 libnl-3-dev libnpth0 libpcre16-3 libpcre3-dev libpcre32-3 libpcrecpp0v5 libprotobuf-c-dev libprotobuf-c1 libprotobuf-dev libprotobuf-lite9v5 libprotobuf9v5 libprotoc-dev libprotoc9v5 libquadmath0 libsigsegv2 libssl-dev libssl-doc libstdc++-5-dev libtool libtsan0 libubsan0 linux-libc-dev lxc-common lxc-dev lxcfs m4 make manpages manpages-dev nih-dbus-tool pinentry-curses pkg-config protobuf-c-compiler protobuf-compiler python-bzrlib python-configobj python-crypto python-dbus python-gi python-gpgme python-httplib2 python-keyring python-launchpadlib python-lazr.restfulclient python-lazr.uri python-oauth python-protobuf python-secretstorage python-simplejson python-wadllib python-zope.interface shared-mime-info uidmap uuid-dev xdg-user-dirs xz-utils zlib1g-dev && \
        add-apt-repository ppa:gophers/archive && \
        apt-get -y update && \
        apt-get -y install golang-1.9 && \
        apt-get -y clean

RUN     update-alternatives --install "/usr/bin/go" "go" "/usr/lib/go-1.9/bin/go" 0 && update-alternatives --set go /usr/lib/go-1.9/bin/go

COPY	sudoers /etc

COPY	run.sh /

RUN	    chmod 777 /root && chmod +x ./run.sh

#RUN     mkdir /root/.cache && chmod 777 /root/.cache

VOLUME  ["/work", "/root/.cache"]

ENTRYPOINT ["./run.sh"]

# vim: ts=4 et nowrap autoindent
