FROM jeeva420/alpine-base
MAINTAINER Jeeva Kailasam <kjeeva@ymail.com>

# Set correct environment variables
ARG BASE_APKLIST="squid curl"

# install main packages
RUN apk update && \
	apk add --no-cache $BASE_APKLIST && \
	rm -rf /var/cache/apk/*

# add local files
COPY /root /
COPY /defaults/squid.conf /etc/squid/squid.conf

# expose ports
EXPOSE 3128
# set volumes
VOLUME /config
VOLUME /var/cache/squid
VOLUME /var/log/squid
