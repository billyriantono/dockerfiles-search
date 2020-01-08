FROM ubuntu:xenial
MAINTAINER Yurii Furko furkoyuriy@gmail.com

ENV ANSIBLE_VERSION=2.4.2.0
ENV DEBIAN_FRONTEND noninteractive

COPY xenial.sources.list /etc/apt/sources.list

RUN apt-get update && \
    apt-get -y upgrade 

RUN apt-get install --no-install-recommends -y \
            software-properties-common \
            apt-utils \
            build-essential

RUN apt-get install -y \
            libffi-dev \
            libssl-dev \
            libffi-dev \
            libssl-dev \
            python-dev \
            python-yaml \
            python-pip \
            python3-dev \
            python3-yaml \
            python3-pip

RUN pip install --upgrade pip
RUN pip install --upgrade cryptography \
                          setuptools \
                          paramiko \
                          pyOpenSSL

RUN pip install ansible==${ANSIBLE_VERSION} ansible-lint

RUN rm -Rf /var/lib/apt/lists/* && \
    rm -Rf /usr/share/doc && \
    rm -Rf /usr/share/man && \
    apt-get clean

RUN useradd -m ansible -s /bin/bash
RUN mkdir /home/ansible/.ssh && \
    touch /home/ansible/.ssh/authorized_keys && \
    chmod 700 /home/ansible/.ssh && \
    chmod 600 /home/ansible/.ssh/authorized_keys &&\
    chown -R ansible:ansible /home/ansible/.ssh

RUN mkdir -p /etc/ansible && \
    echo "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts

VOLUME [ "/sys/fs/cgroup", "/etc/ansible" ]
WORKDIR /etc/ansible

CMD [ "ansible-playbook", "--version" ]
