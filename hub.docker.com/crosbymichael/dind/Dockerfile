FROM ubuntu:17.10

RUN apt-get update && \
	apt-get install -y libseccomp-dev libseccomp2 curl iptables module-init-tools

ADD dockerd /usr/local/bin/dockerd
ADD docker-init /usr/local/bin/docker-init
ADD docker-proxy /usr/local/bin/docker-proxy
