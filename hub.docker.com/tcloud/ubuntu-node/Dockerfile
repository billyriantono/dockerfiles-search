FROM tcloud/ubuntu-python:latest

USER root

ENV NODE_VERSION 7.8.0
ENV NODE_DIR /opt/nodejs

RUN mkdir ${NODE_DIR} && \
	curl -L https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz | tar xvzf - -C ${NODE_DIR} --strip-components=1

ENV PATH $PATH:${NODE_DIR}/bin

VOLUME ["/data","/log"]

WORKDIR /data

CMD ["/sbin/my_init"]

# Clean up
RUN sudo apt-get clean && \
	sudo apt-get autoremove -y && \
	sudo rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*