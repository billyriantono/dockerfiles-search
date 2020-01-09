FROM debian:jessie-slim

LABEL Maintainer="Ernesto Pérez <eperez@isotrol.com>" \
      Name="Docker Debian Ansible" \
      Description="Imágen con la última versión de Ansible" \
      Version="0.1.0"

RUN set -x \
    && sed -i -- 's/main/main contrib non-free/g' /etc/apt/sources.list \
    && apt-get update \
    && apt-get upgrade -y \
    && apt-get install --no-install-recommends -y \
    gnupg \
    ca-certificates

RUN set -x \
    && echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" \
    > /etc/apt/sources.list.d/ansible.list \
    && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 \
    --recv-keys 93C4A3FD7BB9C367 \
    && apt-get update \
    && apt-get install --no-install-recommends -y \
    ansible \
    git \
    python-apt
