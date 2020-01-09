FROM phusion/baseimage:0.9.19

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

ENV DEBIAN_FRONTEND="noninteractive" \
    TERM="xterm"

ADD https://github.com/genielabs/HomeGenie/releases/download/v1.1-beta.519/homegenie-beta_1.1.r519_all.deb /tmp/

ADD homegenie.runit /etc/service/homegenie/run

RUN apt-get -q update && \
	apt-get -qy dist-upgrade && \
	apt-get install -qy --no-install-recommends apt-utils gdebi-core usbutils ca-certificates-mono sudo && \
	gdebi --non-interactive /tmp/homegenie-beta_1.1.r519_all.deb && \
	apt-get -y remove openssh-* gdebi-core && \
	apt-get -y autoremove && \
	apt-get clean -y && \
	chmod +x /etc/service/homegenie/run && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 80

VOLUME /usr/local/bin/homegenie
