FROM ubuntu:bionic-20180821

# change sh from, possibly, dash to bash
RUN cd /bin && rm sh && ln -s bash sh

# apt
RUN apt-get update -y

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
	apt-utils

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
	vim bash-completion sudo

# static analysis, style checking etc packages go below

# user setup
RUN useradd docker -d /home/docker -m -s /bin/bash &&\
 	passwd -d docker &&\
	echo "docker  ALL=(ALL)       NOPASSWD: ALL" >> /etc/sudoers; echo "Defaults    !requiretty" >> /etc/sudoers

USER docker

ENV EXPORT_DIR /export
VOLUME ["$EXPORT_DIR"]
WORKDIR $EXPORT_DIR

#ENTRYPOINT ["tail", "-f", "/dev/null"]

