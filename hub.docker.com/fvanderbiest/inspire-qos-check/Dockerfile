FROM debian:stretch

MAINTAINER fvanderbiest "francois.vanderbiest@gmail.com"

RUN apt-get update && \
    apt-get install -y curl apache2-utils && \
		rm -rf /var/lib/apt/lists/* /usr/share/doc/* /usr/share/man/*

COPY inspire-qos-check /

ENTRYPOINT ["/inspire-qos-check"]
