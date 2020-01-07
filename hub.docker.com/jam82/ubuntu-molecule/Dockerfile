FROM ubuntu:18.04
LABEL maintainer="jam82"

ENV container docker

RUN apt-get update \
    && apt-get install -y \
    apt-utils \
    bash \
    ca-certificates \
    dh-systemd \
    grep \
    iproute2 \
    locales \
    python3 \
    python3-pip \
    rsyslog \
    software-properties-common \
    systemd \
    systemd-cron \
    sudo \
    vim \
    wget \
    && apt-get clean \
    && sed -i 's/^\($ModLoad imklog\)/#\1/' /etc/rsyslog.conf \
    && locale-gen de_DE.UTF-8 \
    && pip3 install ansible \
    && mkdir -p /etc/ansible \
    && echo "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts

COPY initctl_faker .
RUN chmod +x initctl_faker && rm -fr /sbin/initctl && ln -s /initctl_faker /sbin/initctl

VOLUME ["/sys/fs/cgroup", "/tmp", "/run"]

CMD ["/lib/systemd/systemd"]
