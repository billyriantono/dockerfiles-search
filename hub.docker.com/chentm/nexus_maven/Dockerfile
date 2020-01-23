FROM java:openjdk-7-jre
MAINTAINER Timmy (chentm@gmail.com)
ENV REFRESHED_AT 2015-03-12
ENV RUN_AS_USER root
ENV VERSION 2.11.2-04

RUN mkdir -p /runtime
WORKDIR /runtime
RUN wget https://sonatype-download.global.ssl.fastly.net/nexus/oss/nexus-${VERSION}-bundle.tar.gz -O nexus.tar.gz
RUN tar xfz nexus.tar.gz && mv nexus-${VERSION} nexus

COPY nexus.properties /runtime/nexus/conf/

VOLUME /data
EXPOSE 80
CMD ["/runtime/nexus/bin/nexus", "console"]
