FROM marthym/base:1.5.0
LABEL maintainer="marthym@ght1pc9kc.fr" \
      version="1.2.0"

RUN export DEBIAN_FRONTEND=noninteractive && \
	apt -y update && \ 
	apt -y install build-essential python hugo && \
	apt clean && \
	apt autoclean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ARG node=12.13.1
RUN curl -o /tmp/node-${node}-linux-x64.tar.xz "http://nodejs.org/dist/v${node}/node-v${node}-linux-x64.tar.xz" && \
	tar -C /opt -Jxf /tmp/node-${node}-linux-x64.tar.xz && \
	mv /opt/node-v${node}-linux-x64 /opt/nodejs && \
	ln -s /opt/nodejs/bin/node /usr/local/bin/node && \
	ln -s /opt/nodejs/bin/npm /usr/local/bin/npm && \
	rm -rf /tmp/node-${node}-linux-x64.tar.xz

RUN npm -g install gulp && \
	ln -s /opt/nodejs/bin/gulp /usr/local/bin/gulp
