FROM ubuntu:18.04

MAINTAINER Carlos Rodríguez <nidr0x@gmail.com>


RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        python python-yaml sudo python-wheel python-pip \
        python-setuptools software-properties-common && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /usr/share/doc && rm -rf /usr/share/man && \
    apt-get clean && \
    pip install ansible pywinrm cryptography && \
    mkdir -p /etc/ansible && \
    echo 'localhost' > /etc/ansible/hosts
    

