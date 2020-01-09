# kentwait/picard
FROM kentwait/alpine-oraclejdk8
MAINTAINER Kent Kawashima <kentkawashima@gmail.com>

ENV PICARD_VERSION 2.8.3

ADD https://github.com/broadinstitute/picard/releases/download/${PICARD_VERSION}/picard.jar /opt

ENV PICARD /opt/picard.jar

WORKDIR /data
VOLUME /data
ENTRYPOINT ["/init", "java", "-jar", "/opt/picard.jar"]
