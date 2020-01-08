FROM ubuntu:16.04

RUN dpkg --add-architecture i386 && apt-get update

RUN apt-get install -y wget perl git gcc gcc-multilib libc6 libc6-dev libc6-dev-i386 \
    linux-libc-dev libstdc++5 libstdc++-5-dev python2.7 libpcap-dev libarchive-dev \
    make automake autoconf libtool libssl1.0.0 libssl-dev libpcre3 libpcre3-dev gdb \
    flex bison libtool dejagnu e2fsprogs tcl libxml2 libxml2-dev zlib1g zlib1g-dev \
    libncurses5-dev mscgen autoconf-archive ntp pkgconf codespell dos2unix \
    g++ libconfig-dev locales squashfs-tools \
    lib32z1 libxml2:i386 libxml2-dev:i386

RUN apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/

RUN wget https://cpan.metacpan.org/authors/id/W/WB/WBRASWELL/Parse-Yapp-1.2.tar.gz && \
    tar xvf Parse-Yapp-1.2.tar.gz && \
    (cd Parse-Yapp-1.2 && perl Makefile.PL && make && make install) && \
	rm -rf Parse-Yapp-1.2.tar.gz Parse-Yapp-1.2

RUN locale-gen en_US.UTF-8
