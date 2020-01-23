FROM debian:buster-slim

MAINTAINER Gerolf Ziegenhain "gerolf.ziegenhain@gmail.com"

RUN apt-get update
RUN apt-get -y install socat libhamlib-utils
RUN apt-get -qqy autoclean && rm -rf /tmp/* /var/tmp/*

ENV RIGSERVER 10.101.10.53
ENV RIGSERVER_PTT_PORT 3003
ENV RIGSERVER_CAT_PORT 3002
ENV RIGMODEL 133

ADD startup.sh /bin

HEALTHCHECK --interval=10s --timeout=3s CMD rigctl -m $RIGMODEL -r /dev/YPort f ||exit 1

ENTRYPOINT ["startup.sh"]
CMD ["bash"]
