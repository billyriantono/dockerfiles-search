FROM ubuntu:16.04
MAINTAINER yann.xia<me.yan.xia@qq.com>

# Add custom china source
#ADD sources.list /etc/apt/

# instal tcpdump
RUN apt update; apt install -y tcpdump netcat curl net-tools iproute inetutils-ping traceroute

CMD ["sleep", "1000"]
