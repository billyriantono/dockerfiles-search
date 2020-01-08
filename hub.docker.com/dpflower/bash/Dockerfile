#
# Dockerfile for bash
#

FROM bash

MAINTAINER kev <dongpingmax@163.com>

# ENV TOKEN 00000000-0000-0000-0000-000000000000

ENV LC_ALL=en_US.UTF-8

#RUN set -xe \
#    && apk add -U aria2 \
#    && rm -rf /var/cache/apk/* \
#    && aria2c https://github.com/tianon/gosu/releases/download/1.10/gosu-amd64 -o /usr/local/bin/gosu \
#    && chmod +x /usr/local/bin/gosu \
#    && adduser -D aria2

VOLUME /home/aria2 /etc/aria2

EXPOSE 6800

WORKDIR /root

#CMD set -xe \
#    && chown -R aria2:aria2 /home/aria2 \
#    && chown -R aria2:aria2 /etc/aria2  
	
	
	
