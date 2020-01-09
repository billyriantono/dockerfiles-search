# Version: 0.0.1
#FROM java:8
FROM frolvlad/alpine-oraclejdk8:latest
MAINTAINER Paul Ambrose "pambrose@mac.com"

VOLUME ["/haptava/conf"]

ADD http://downloads.haptava.io/releases/0.9.39/log4j/webdav.log4j.properties /haptava/log4j/
ADD http://downloads.haptava.io/releases/0.9.39/lib/webdav.jar /haptava/lib/

EXPOSE 8080

WORKDIR /haptava

ENV HAPTAVA_HOME /haptava

ENTRYPOINT ["java", \
            "-Dlog4j.configuration=file:./log4j/webdav.log4j.properties", \
            "-jar", "./lib/webdav.jar"]

# docker run -it --entrypoint=/bin/bash haptava/webdav:0.9.39
# docker run -d haptava/webdav:0.9.39 -u fred -p topsecret
