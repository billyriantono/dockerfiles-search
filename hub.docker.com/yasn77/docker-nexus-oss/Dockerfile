FROM ubuntu:14.04
MAINTAINER Yasser Nabi "yassersaleemi@gmail.com"
VOLUME ["/sonatype-nexus"]
ENV PLEXUS_NEXUS_WORK /sonatype-nexus
ENV TZ Europe/London
ENV DEBIAN_FRONTEND noninteractive
EXPOSE 8081 2812 22

RUN sed 's/main$/main universe/' -i /etc/apt/sources.list && \
        apt-get update && \
        apt-get -y install \
            monit \
            curl \
            openjdk-7-jre-headless

ADD ./monit.d/ /etc/monit/conf.d/
ADD ./start.sh /start.sh
ADD ./start-nexus.sh /start-nexus.sh

RUN curl -L -s http://www.sonatype.org/downloads/nexus-latest-bundle.tar.gz | tar -C /opt/ -zxvf - ; \
      ln -s /opt/nexus* /opt/nexus ; \
      mkdir -p /opt/nexus/piddir ; \
      sed -e 's%^#\?\(PIDDIR\).*%\1=/opt/nexus/piddir%' -i /opt/nexus/bin/nexus 

ENTRYPOINT ["/bin/bash", "/start.sh"]
