FROM ubuntu:14.04
MAINTAINER Mehmet Mersin <mmersin@gmail.com>

ENV PKG_INSTALL="apt-get install --no-install-recommends -y"

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive ${PKG_INSTALL} software-properties-common && \
    apt-add-repository ppa:ansible/ansible && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive ${PKG_INSTALL} ansible && \
    DEBIAN_FRONTEND=noninteractive ${PKG_INSTALL} python-pip && \
    DEBIAN_FRONTEND=noninteractive ${PKG_INSTALL} openssh-client && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN echo '[local]\nlocalhost\n' > /etc/ansible/hosts

RUN pip install boto
