FROM debian:jessie

MAINTAINER Martijn Vermaat <martijn@vermaat.name>

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update

# Configure locales
RUN apt-get install -y locales \
 && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
 && locale-gen en_US.utf8 \
 && /usr/sbin/update-locale LANG=en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8

# Install some common dependencies and Ansible
RUN apt-get install -y sudo curl git python-pip python-dev \
 && pip install ansible==2.0.1 markupsafe

CMD ["/bin/bash"]
