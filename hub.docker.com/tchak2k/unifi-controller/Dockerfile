FROM debian:8.0


ENV DEBIAN_FRONTEND noninteractive

VOLUME ["/usr/lib/unifi/data"]

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv C0A52C50

ADD 100-ubnt.list /etc/apt/sources.list.d/100-ubnt.list
RUN apt-get update
RUN apt-get install -y unifi

WORKDIR /var/lib/unifi

EXPOSE 8080/tcp 8081/tcp 8443/tcp 8843/tcp 8880/tcp 3478/udp

ENTRYPOINT ["/usr/bin/java", "-Xmx1024M", "-jar", "/usr/lib/unifi/lib/ace.jar"]
CMD ["start"]
