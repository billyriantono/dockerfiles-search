FROM debian:jessie

RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install -y -o "APT::Install-Recommends=yes" \
        systemd \
        systemd-sysv

ENV container docker

STOPSIGNAL SIGRTMIN+3

ENTRYPOINT [ "/sbin/init" ]
