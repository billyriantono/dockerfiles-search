# gotchas/pharo-base64
FROM debian:9
#FROM ubuntu:16.04
#FROM ubuntu:14.04
MAINTAINER CAs

RUN apt-get update -q
RUN apt-get -qy --no-install-recommends install \
	libfreetype6 \
        curl \
	libcurl3-gnutls \
	libcairo2 \
	unixodbc \
        unzip \
	ca-certificates \
	git \
	iputils-ping \
	nano \
	telnet

RUN apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#CMD ["/opt/pharo","Pharo.image","--no-quit"]
CMD ["./pharo-run","--no-quit"]

RUN echo "Dependencies for Pharo are installed"
