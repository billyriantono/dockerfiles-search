FROM jenkins/jenkins:lts

ENV DEBIAN_FRONTEND noninteractive

USER root

RUN apt-get update \
	&& apt-get install -y \
	lsb-core \
	lsb-release \
	&& rm -rf /var/lib/apt/lists/*

# http://docs.ansible.com/ansible/latest/intro_installation.html#latest-releases-via-apt-debian
RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list
RUN	apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
RUN	apt-get update
RUN apt-get install -y ansible
