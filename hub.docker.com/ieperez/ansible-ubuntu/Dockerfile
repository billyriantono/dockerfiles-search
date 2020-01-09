FROM ubuntu:xenial

LABEL Maintainer="Ernesto Pérez <eperez@isotrol.com>" \
      Name="Docker Ubuntu 18.04 Xenial Ansible" \
      Description="Imágen con la última versión de Ansible" \
      Version="0.1.0"

RUN set -x \
    && apt-get update \
    && apt-get upgrade -y \
    && apt-get install --no-install-recommends -y \
    gnupg \
    ca-certificates

RUN set -x \
    && echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu xenial main" \
    > /etc/apt/sources.list.d/ansible.list \
    && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 \
    --recv-keys 93C4A3FD7BB9C367 \
    && apt-get update \
    && apt-get install --no-install-recommends -y \
    ansible \
    git \
    python-apt
