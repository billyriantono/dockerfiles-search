FROM ubuntu:18.04
MAINTAINER Kevin Coakley <kcoakley@sdsc.edu>

RUN apt-get update && \
    apt-get install --no-install-recommends -y software-properties-common && \
    apt-add-repository ppa:ansible/ansible && \
    apt-get update && \
    apt-get install -y ansible=2.5.3-1ppa~bionic && \
    rm -rf /var/lib/apt/lists/*

RUN echo '[local]\nlocalhost\n' > /etc/ansible/hosts
