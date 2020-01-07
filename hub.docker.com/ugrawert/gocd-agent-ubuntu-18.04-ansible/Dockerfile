# Dockerfile

FROM gocd/gocd-agent-ubuntu-18.04:v19.5.0

MAINTAINER Uwe Grawert

LABEL description="GoCD Agent with Ansible"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get --yes update && \
    apt-get --yes dist-upgrade
RUN apt-get --yes --no-install-recommends --no-install-suggests install \
        ansible
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
