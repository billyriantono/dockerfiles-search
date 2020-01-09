FROM debian:jessie
MAINTAINER Anders B. Hansen <anders@birkoe.com>

ENV DEBIAN_FRONTEND noninteractive

VOLUME ["/var/lib/unifi", "/var/log/unifi", "/var/run/unifi"]

EXPOSE 8080/tcp 8081/tcp 8443/tcp 8880/tcp 3478/udp

RUN apt-get -y update && \
	apt-get -y upgrade && \
	apt-get install -y --force-yes --no-install-recommends \
		jsvc \
		binutils \
		mongodb-server \
		openjdk-7-jre-headless && \
	apt-get -y clean && \
	rm -rf /var/lib/apt/lists/*

ADD http://dl.ubnt.com/unifi/5.6.29/unifi_sysvinit_all.deb /unifi.deb

RUN dpkg -i unifi.deb && rm unifi.deb

ENTRYPOINT ["/usr/bin/java", "-Xmx1024M", "-jar", "/usr/lib/unifi/lib/ace.jar"]
CMD ["start"]
