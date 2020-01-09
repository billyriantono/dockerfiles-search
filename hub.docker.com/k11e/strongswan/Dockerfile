FROM ubuntu:14.04

MAINTAINER jet tsang <zeon-git@jettsang.com>
ADD ./bin/* /usr/bin/
VOLUME /etc

RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y upgrade && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install strongswan strongswan-ikev2 strongswan-plugin-* iptables

CMD /usr/bin/start-vpn
