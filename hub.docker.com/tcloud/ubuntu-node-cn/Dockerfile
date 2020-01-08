# Version 1.3

FROM tcloud/ubuntu-python:latest
MAINTAINER tcloud

RUN useradd -ms /bin/bash node && \
    chown -R node /usr/local && \
    echo "ALL	ALL = (ALL) NOPASSWD: ALL" >> /etc/sudoers

USER node

ENV NODE_VERSION 4.2.4
ENV NVM_DIR /home/node/.nvm

RUN curl https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash

RUN . /home/node/.nvm/nvm.sh && \
	nvm install $NODE_VERSION && \
	nvm alias default $NODE_VERSION && \
	npm install -g bower gulp request strongloop strong-pm nrm && \
	mkdir /home/node/pm && \
	nrm use taobao

VOLUME ["/data","/log"]

WORKDIR /data

CMD ["/sbin/my_init"]

RUN sudo apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*