FROM debian:buster

ENV container=docker \
    LC_ALL=C \
    DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && \
    apt-get upgrade -y &&\
    apt-get install -y systemd udev vim-tiny && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
    
RUN mkdir /etc/systemd/system/systemd-networkd.service.d/ && \
    printf "[Service]\nEnvironment=SYSTEMD_LOG_LEVEL=debug" > /etc/systemd/system/systemd-networkd.service.d/10-debug.conf && \
    \
    sed -i 's/#\(ForwardToConsole=\).*$/\1yes/' /etc/systemd/journald.conf && \
    sed -i '/^IPAddressDeny=/s/^s/#/' /lib/systemd/system/systemd-journald.service && \
    systemctl set-default multi-user.target && \
    systemctl enable systemd-udevd.service systemd-networkd.service && \
    \
    # Don't start any optional services except for the few we need.
    # Source: https://github.com/solita/docker-systemd/blob/a87ced841eeb831a0d0ee5d03d03681f04dcf231/Dockerfile
    find /etc/systemd/system \
         /lib/systemd/system \
         -path '*.wants/*' \
         -not -name '*udevd*' \
         -not -name '*networkd*' \
         -not -name '*journald*' \
         -not -name '*systemd-tmpfiles*' \
         -not -name '*systemd-user-sessions*' \
        | tee /dev/stderr | xargs rm

# systemd signal spec: https://github.com/systemd/systemd/blob/master/src/core/manager.c#L445
STOPSIGNAL "RTMIN+3"

ENTRYPOINT ["/lib/systemd/systemd"]
