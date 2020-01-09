FROM centos:centos8
LABEL maintainer="joe@zollo.net"

RUN dnf update -y && dnf clean all
RUN dnf install python3-devel python3 python3-pip gcc git -y && dnf clean all
RUN pip3 install ansible molecule
RUN mkdir -p /etc/ansible/ && echo "[local]" > /etc/ansible/hosts && echo 'localhost ansible_connection=local' >> /etc/ansible/hosts

ENTRYPOINT [ "/bin/bash" ]
