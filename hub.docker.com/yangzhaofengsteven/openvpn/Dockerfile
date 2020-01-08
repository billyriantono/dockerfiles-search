FROM debian:stable

MAINTAINER Steven Yang <yangzhaofengsteven@gmail.com>

#ADD . $ASSETS_DIR

#EXPOSE 1194/tcp 1194/udp

VOLUME /etc/openvpn

RUN apt update && apt install -y openvpn libgcrypt20 && apt clean

CMD ["/usr/sbin/openvpn", "--cd", "/etc/openvpn/", "--config", "server.conf"]

