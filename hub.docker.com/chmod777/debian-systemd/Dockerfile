FROM debian:stretch

ENV LC_ALL C
ENV DEBIAN_FRONTEND noninteractive
ENV container docker

RUN apt-get update \
    && apt-get install -y systemd \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# From solita/docker-systemd
RUN find /etc/systemd/system \
    /lib/systemd/system \
    -path '*.wants/*' \
    -not -name '*journald*' \
    -not -name '*systemd-tmpfiles*' \
    -not -name '*systemd-user-sessions*' \
    -not -name '*dbus.service' \
    -exec rm \{} \;

RUN systemctl set-default multi-user.target

VOLUME [ "/sys/fs/cgroup" ]

CMD [ "/lib/systemd/systemd" ]