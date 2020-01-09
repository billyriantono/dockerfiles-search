FROM debian:latest

LABEL maintainer="denis@generic.business"

RUN apt-get update \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -y \
	iperf3

EXPOSE 5201/udp 5201/tcp

ENTRYPOINT ["/usr/bin/iperf3","-s"]
