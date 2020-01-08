FROM amd64/maven:3.5-jdk-8-alpine

RUN apk add --no-cache \
    xmlstarlet git openssh rsync

COPY .m2/settings.xml /root/.m2/settings.xml
