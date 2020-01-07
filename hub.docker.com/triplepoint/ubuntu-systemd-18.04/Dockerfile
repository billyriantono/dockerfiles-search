FROM ubuntu:18.04
LABEL maintainer="Jonathan Hanson (jonathan@jonathan-hanson.org)"

ENV container docker

# Don't start any optional services except for the few we need.
RUN find /etc/systemd/system \
         /lib/systemd/system \
         -path '*.wants/*' \
         -not -name '*journald*' \
         -not -name '*systemd-tmpfiles*' \
         -not -name '*systemd-user-sessions*' \
         -exec rm \{} \;

# CA Certificates and openssl - support TLS
# curl - supports some ansible fallback assumptions
# net tools - support testinfra during role testing
# ssh - so we can talk to the instance with Ansible
RUN apt-get update && apt-get install -y \
        ca-certificates \
        dbus \
        curl \
        net-tools \
        openssl \
        python \
        ssh \
        systemd \
        tzdata \
    && rm -rf /var/lib/apt/lists/*

# Make sure Pip and friends are up to the latest version.
ADD https://bootstrap.pypa.io/get-pip.py /tmp/
RUN python /tmp/get-pip.py \
    && rm /tmp/get-pip.py

RUN systemctl set-default multi-user.target
RUN systemctl mask dev-hugepages.mount sys-fs-fuse-connections.mount

STOPSIGNAL SIGRTMIN+3

# Workaround for docker/docker#27202, technique based on comments from docker/docker#9212
CMD ["/bin/bash", "-c", "exec /sbin/init --log-target=journal 3>&1"]
