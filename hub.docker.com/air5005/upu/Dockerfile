FROM centos:latest

RUN yum install -y epel-release

RUN yum install -y pciutils \
	&& yum install -y tcpdump \
	&& yum install -y ethtool \
	&& yum install -y hiredis-devel \
	&& yum install -y net-tools \
	&& yum install -y redhat-lsb \
	&& yum install -y tcpreplay msgpack-devel \
	&& yum install -y readline-devel libedit-devel \
	&& yum install -y gcc automake autoconf libtool make \
	&& yum install -y glibc-static libstdc++-static libevent-devel \
	&& yum install -y iproute numactl mbedtls gdb numactl-devel numactl-libs

WORKDIR /opt/upu-5G
