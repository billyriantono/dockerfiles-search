FROM debian:latest

MAINTAINER moeyard TRAN "moeyard@moeyard.com"

ARG FRP_VERSION=0.30.0

WORKDIR /tmp
RUN 	set -x && \
	apt update && \
	apt  install -y wget && \
	wget https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_amd64.tar.gz &&  \
	tar -zxf frp_${FRP_VERSION}_linux_amd64.tar.gz && \
	mv frp_${FRP_VERSION}_linux_amd64 /var/frp && \
	mkdir -p /var/frp/conf &&  \
	apt remove -y wget && \
 	apt autoremove -y && \
	apt clean  && \
	rm -rf /var/lib/apt/lists/*

VOLUME /var/frp/conf 

WORKDIR /var/frp
ENTRYPOINT ./frpc -c ./conf/frpc.ini
