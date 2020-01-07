FROM debian:jessie
LABEL maintainer="jam82"

ENV container docker

RUN apt-get update && apt-get install -y \
    bash \
    ca-certificates \
    dh-systemd \
    grep \
    iproute2 \
    python \
    python-pip \
    rsyslog \
    software-properties-common \
    systemd \
    systemd-cron \
    sudo \
    vim \
    wget \
    && apt-get clean \
    && sed -i 's/^\($ModLoad imklog\)/#\1/' /etc/rsyslog.conf \
    && pip install ansible \
    && mkdir -p /etc/ansible \
    && echo -e '[local]\nlocalhost ansible_connection=local' > /etc/ansible/hosts

VOLUME ["/sys/fs/cgroup"]

CMD ["/lib/systemd/systemd"]
