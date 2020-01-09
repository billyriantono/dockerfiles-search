FROM ubuntu:18.04


MAINTAINER joaniznardo (github)

RUN apt-get update && apt-get install -y debconf-utils iproute2 traceroute iputils-ping iputils-arping isc-dhcp-client resolvconf openssh-server sudo tcpdump inotify-tools dnsutils supervisor && useradd -m ubuntu && echo "ubuntu:ubuntu" | chpasswd && adduser ubuntu sudo

CMD /etc/init.d/ssh restart && supervisord -n

