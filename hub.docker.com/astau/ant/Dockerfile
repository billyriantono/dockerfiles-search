# apache ant image
FROM astau/openjdk:latest

MAINTAINER Srikanth <srikanth@astau.com>

RUN apk add apache-ant --update-cache --repository http://dl-4.alpinelinux.org/alpine/edge/community/ --allow-untrusted \
	&& rm -rf /var/cache/apk/*

ENV ANT_HOME /usr/share/java/apache-ant
ENV PATH $PATH:$ANT_HOME/bin
CMD ["ant", "-version"]