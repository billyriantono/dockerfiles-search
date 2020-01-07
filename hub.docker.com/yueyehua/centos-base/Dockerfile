FROM centos:7
MAINTAINER Richard Delaplace "rdelaplace@yueyehua.net"
LABEL version="1.0.0"

# Install basic packages and common dependencies
RUN \
  yum -y install \
    openssl-devel libyaml-devel readline-devel zlib-devel ncurses-devel \
    libffi-devel gdbm-devel sudo git redhat-lsb-core;

# Clean all
RUN \
  yum clean all;

VOLUME ["/sys/fs/cgroup"]
CMD  ["/lib/systemd/systemd"]
