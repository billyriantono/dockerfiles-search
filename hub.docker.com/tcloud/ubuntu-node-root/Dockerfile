FROM tcloud/ubuntu-python:latest

USER root

ENV NODE_VERSION 6.1.0
ENV NVM_DIR /root/.nvm

RUN curl https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash && \
	. /root/.nvm/nvm.sh && \
	nvm install $NODE_VERSION && \
	nvm alias default $NODE_VERSION

VOLUME ["/data","/log"]

WORKDIR /data

CMD ["/sbin/my_init"]

# Clean up
RUN sudo apt-get clean && \
	sudo apt-get autoremove -y && \
	sudo rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*