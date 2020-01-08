# Version 1.3

FROM tcloud/ubuntu-node:4.2.4
MAINTAINER tcloud

USER node

WORKDIR /data

RUN sudo chown -R node:node /usr/local && \
	mkdir /home/node/pm && \
	sudo mkdir /etc/service/pm && \
	. /home/node/.nvm/nvm.sh && \
	nvm alias default $NODE_VERSION && \
	npm install -g strong-pm && \
	npm cache clear

ADD files/pm.sh /etc/service/pm/run

VOLUME ["/data","/log"]

# Expose pm port
EXPOSE 8701 3000 3001 3002 3003

CMD ["/sbin/my_init"]

RUN sudo apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*