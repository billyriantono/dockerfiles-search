FROM ubuntu:trusty

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA5DFFC && \
    echo 'deb http://apt.sonarr.tv/ master main' > /etc/apt/sources.list.d/nzbdrone.list && \
    apt-get update -q && \
    apt-get install -qy libmono-cil-dev nzbdrone

ADD start.sh /start.sh

VOLUME ["/data"]
EXPOSE 8989

CMD ["/start.sh"]
