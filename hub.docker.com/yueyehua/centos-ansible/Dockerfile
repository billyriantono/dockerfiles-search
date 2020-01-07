FROM yueyehua/centos-python:latest
MAINTAINER Richard Delaplace "rdelaplace@yueyehua.net"
LABEL version="1.0.0"

# Install Ansible and linters
RUN \
  pip3 install ansible ansible-lint;

# Mask failing services
RUN \
  systemctl mask -- \
    sys-fs-fuse-connections.mount \
    dev-hugepages.mount \
    systemd-tmpfiles-setup.service;

VOLUME ["/sys/fs/cgroup", "/run", "/run/lock"]
CMD  ["/lib/systemd/systemd"]
