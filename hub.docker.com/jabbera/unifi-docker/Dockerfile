FROM debian:jessie
MAINTAINER Jacob Alberty <jacob.alberty@foundigital.com>

VOLUME ["/var/lib/unifi"]

ENV DEBIAN_FRONTEND noninteractive

RUN echo "deb http://www.ubnt.com/downloads/unifi/distros/deb/debian debian ubiquiti" \
  > /etc/apt/sources.list.d/20ubiquiti.list
RUN echo "deb http://downloads-distro.mongodb.org/repo/debian-sysvinit dist 10gen" \
  > /etc/apt/sources.list.d/21mongodb.list

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv C0A52C50
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10

RUN apt-get -q update && \
    apt-get install -qy --force-yes unifi-beta=4.6.3-4850 && \
    apt-get -q clean && \
    rm -rf /var/lib/apt/lists/*

EXPOSE 8080/tcp 8081/tcp 8443/tcp 8843/tcp 8880/tcp 3478/udp

## Uncommenting these allows unifi to run as user nobody but I don't know for sure that all features work so leaving commented out for now
#RUN chown -R nobody.nogroup /usr/lib/unifi
#RUN chown -R nobody.nogroup /var/lib/unifi
#RUN chown -R nobody.nogroup /var/log/unifi
#RUN chown -R nobody.nogroup /var/run/unifi
#USER nobody

WORKDIR /var/lib/unifi

ENTRYPOINT ["/usr/bin/java", "-Xmx1024M", "-jar", "/usr/lib/unifi/lib/ace.jar"]
CMD ["start"]
