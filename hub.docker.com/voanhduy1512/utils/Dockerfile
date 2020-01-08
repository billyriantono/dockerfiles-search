FROM ubuntu:17.10

RUN apt update && apt install -y vim curl jq telnet dnsutils && \
	apt-get clean autoclean && \
	apt-get autoremove -y && \
	rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log

ADD pdf-sample.pdf /tmp
