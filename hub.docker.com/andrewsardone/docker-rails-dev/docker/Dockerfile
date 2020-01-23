FROM ubuntu:xenial
MAINTAINER Andrew Glass <andrew.glass@outlook.com>

VOLUME ["/var/lib/unifi", "/var/log/unifi", "/var/run/unifi"]

RUN echo "deb http://www.ubnt.com/downloads/unifi/debian unifi5 ubiquiti" \
  > /etc/apt/sources.list.d/20ubiquiti.list && \
  apt-key adv --keyserver keyserver.ubuntu.com --recv C0A52C50

RUN apt-get -q update && \
    apt-get install -qy --force-yes unifi

EXPOSE 8080/tcp 8081/tcp 8443/tcp 8843/tcp 8880/tcp 3478/udp

WORKDIR /var/lib/unifi

ENTRYPOINT ["/usr/bin/java", "-Xmx1024M", "-jar", "/usr/lib/unifi/lib/ace.jar"]
CMD ["start"]

