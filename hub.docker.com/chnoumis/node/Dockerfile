FROM chnoumis/base:2.0.0

MAINTAINER chnoumis

# User root user to install software
USER root

RUN apk add --update \
	binutils-gold \
	ca-certificates \
	curl \
	git \
	gcc \
	g++ \
	libgcc \
	libstdc++ \
	linux-headers \
	make \
	paxctl \
	python

RUN update-ca-certificates

RUN curl -sSL https://nodejs.org/dist/v6.2.0/node-v6.2.0.tar.gz | tar -xz && \
  cd node-v6.2.0 && \
  ./configure --prefix=/usr && \
  NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
  make out/Makefile && \
  make -j${NPROC} -C out mksnapshot && \
  paxctl -cm out/Release/mksnapshot && \
  make -j${NPROC} && \
  make install && \
  paxctl -cm /usr/bin/node && \
  cd / && \
  rm -rf /etc/ssl node-v6.2.0 \
    /usr/share/man /tmp/* /var/cache/apk/* /root/.npm /root/.node-gyp \
    /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html

# Create node directory
RUN mkdir -p /opt/chnoumis/node/app
RUN mkdir -p /opt/chnoumis/node/bin
RUN mkdir -p /opt/chnoumis/node/build

RUN chown -R chnoumis:chnoumis /opt/chnoumis/node

ADD deploy-and-start /usr/bin/deploy-and-start

USER chnoumis

# Set the working directory
WORKDIR /opt/chnoumis/node/app

CMD "/usr/bin/deploy-and-start"