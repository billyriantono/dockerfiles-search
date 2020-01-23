FROM ubuntu:latest
MAINTAINER coollee <ssangyop@gmail.com>

RUN apt-get update && apt-get dist-upgrade -y && \
	apt-get autoclean && apt-get --purge -y autoremove && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
