FROM ubuntu:18.04

RUN DEBIAN_FRONTEND=noninteractive; apt-get update && \
        apt-get -y install \
	wget \
	curl \
	httpie \
	iputils-ping \
	mtr \
	traceroute \
	iproute2 \
	telnet \
	tcpdump \
	wireshark \
	net-tools

CMD ["/bin/bash"]
