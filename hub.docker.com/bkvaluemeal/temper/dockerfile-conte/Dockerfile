FROM ubuntu:16.04

MAINTAINER bjddd192 <bjddd192@163.com>

RUN apt-get update  && \
	apt-get -y install wget libappindicator3-1 && \
	wget https://raw.githubusercontent.com/getlantern/lantern-binaries/master/lantern-installer-64-bit.deb && \
	dpkg -i lantern-installer-64-bit.deb && \
	rm -rf lantern-installer-64-bit.deb && \
	apt-get -f install && \
	apt-get clean && \
	rm -rf /var/cache/apt/* /var/lib/apt/lists/*

ENV TZ "Asia/Shanghai"
ENV TERM linux

EXPOSE 8087/tcp 8080/tcp

ENTRYPOINT ["/usr/bin/lantern", "--configdir=/root", "--headless=true", "--proxyall=true", "--startup=false", "--clear-proxy-settings=false", "--addr=0.0.0.0:8087", "--uiaddr=0.0.0.0:8080"]
