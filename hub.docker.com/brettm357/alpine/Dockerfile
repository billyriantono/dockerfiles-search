FROM alpine:latest
MAINTAINER brettm357@me.com

ENV DEBIAN_FRONTEND noninteractive
ENV HOME /root
ENV UNIFI_VERSION 5.6.2-224554000b

#RUN @testing http://nl.alpinelinux.org/alpine/edge/testing

RUN echo http://nl.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories && \

    apk upgrade --update && \

 #   apk --no-cache add \
 #   curl \
 #   mongodb \
 #   openjdk8-jre \
    apk add --no-cache --virtual=build-dependencies \
	curl \
	unzip && \

 # INSTALL RUNTIME PACKAGES
    apk add --no-cache \
	openjdk8-jre-base \
	supervisor \
	mongodb && \

 # INSTALL UNIFI
   mkdir -p /opt && \
   #cd ~ && wget http://dl.ubnt.com/unifi/5.3.8/UniFi.unix.zip
   #unzip -q UniFi.unix.zip -d /opt
   #chown -R ubnt:ubnt /opt/UniFi

    curl -o \
    /tmp/unifi.zip -L "https://www.ubnt.com/downloads/unifi/$UNIFI_VERSION/UniFi.unix.zip" && \
    unzip /tmp/unifi.zip -d /opt && \
    
 # CLEANUP
    apk del --purge \
    build-dependencies && \
    rm -rf /tmp/*
    
VOLUME /usr/lib/unifi/data
    
WORKDIR /usr/lib/unifi

    # ADD SUPERVISOR CONFIG
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["/usr/bin/supervisord"]
#,"--configuration=/etc/supervisor/supervisord.conf"]






