FROM alpine:3.6
MAINTAINER Simon Waite <opless@gmail.com>
#########################################################################
# Simon Waite                              Sat 12 Aug 2017 09:20:51 BST #
# opless@gmail.com                                                      #
#########################################################################
#
# Stub Dockerfile for creating Dockerfiles with ansible
# 
# Ideas borrowed from https://github.com/philm/ansible_playbook
#
#
#########################################################################

ENV HOME /root

# Enusure we're update, have a minimal dev environment,
# Then get/update pip, as various distros are old/get fiddled with.
# Install latest ansible and set things up for localhost.

RUN apk add --update \ 
            build-base \
            libffi-dev \
            python2 \
            python2-dev \
            py-pip \
            py-openssl \
            wget \
            curl \
            git && \
    pip install --upgrade pip  && \
    pip install ansible  && \
    mkdir /etc/ansible/ /ansible  && \
    echo "[local]" >> /etc/ansible/hosts  && \
    echo "localhost" >> /etc/ansible/hosts  && \
    mkdir -p /work  

WORKDIR /work

ENV ANSIBLE_GATHERING smart
ENV ANSIBLE_HOST_KEY_CHECKING false
ENV ANSIBLE_RETRY_FILES_ENABLED false
ENV ANSIBLE_ROLES_PATH /ansible/playbooks/roles
ENV ANSIBLE_SSH_PIPELINING True
