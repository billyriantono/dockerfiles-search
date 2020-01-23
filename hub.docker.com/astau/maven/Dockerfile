# Maven 3 image
FROM astau/openjdk:latest

MAINTAINER Srikanth <srikanth@astau.com>

RUN apk add maven --update-cache --repository http://dl-4.alpinelinux.org/alpine/edge/community/ --allow-untrusted \
	&& rm -rf /var/cache/apk/*

ENV MAVEN_HOME /usr/share/java/maven-3
ENV PATH $PATH:$MAVEN_HOME/bin

CMD ["mvn"]