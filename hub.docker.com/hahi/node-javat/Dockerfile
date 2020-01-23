FROM maven:3.6.1-jdk-8-alpine

##### install third-party packages #####

COPY ./utils/alpinelinux/repositories /etc/apk/repositories

RUN apk --update add --no-cache make curl

##### use mirror for settings #####

COPY maven/settings.xml /usr/share/maven/conf/
