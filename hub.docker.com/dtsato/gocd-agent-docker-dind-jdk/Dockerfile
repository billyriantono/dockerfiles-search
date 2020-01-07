FROM gocd/gocd-agent-docker-dind:v19.11.0
MAINTAINER Danilo Sato <dtsato@gmail.com>

USER root

RUN apk add --no-cache openjdk11

USER go

ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk
ENV PATH $PATH:/usr/lib/jvm/java-11-openjdk/bin
