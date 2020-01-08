FROM debian:latest

ENV DEBIAN_FRONTEND noninteractive

RUN rm /etc/localtime  \
	&& ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime

RUN apt-get update \
	&& apt-get install -y curl \
  	&& rm -rf /var/lib/apt/list*

ENTRYPOINT /bin/bash
