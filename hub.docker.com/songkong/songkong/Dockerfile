FROM openjdk:8-jre-alpine

RUN apk --no-cache add \
      ca-certificates \
      curl \
      fontconfig \
      msttcorefonts-installer \
      tini \
 && update-ms-fonts \
 && fc-cache -f
    
RUN mkdir -p /opt \
 && curl http://www.jthink.net/songkong/downloads/current/songkong-linux-docker.tgz?val=112 | tar -C /opt -xzf - \
&& find /opt/songkong -perm /u+x -type f -print0 | xargs -0 chmod a+x

EXPOSE 4567

ENTRYPOINT ["/sbin/tini"]

# Config, License, Logs, Reports and Internal Database
VOLUME /songkong

# Music folder should be mounted here
VOLUME /music

WORKDIR /opt/songkong

CMD /opt/songkong/songkongremote8.sh