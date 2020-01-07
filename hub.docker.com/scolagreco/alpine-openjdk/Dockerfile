FROM scolagreco/alpine-base:v3.9.2

ENV JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk
ENV JRE_HOME=$JAVA_HOME/jre
ENV PATH=$PATH:$JAVA_HOME/bin

RUN apk add --update --no-cache openjdk8

# Metadata params
ARG BUILD_DATE
ARG VERSION="1.8.0_212"
ARG VCS_URL="https://github.com/scolagreco/alpine-openjdk.git"
ARG VCS_REF

# Metadata
LABEL maintainer="Stefano Colagreco <stefano@colagreco.it>" \
        org.label-schema.name="Alpine + Java (OpenJDK)" \
        org.label-schema.build-date=$BUILD_DATE \
        org.label-schema.version=$VERSION \
        org.label-schema.vcs-url=$VCS_URL \
        org.label-schema.vcs-ref=$VCS_REF \
        org.label-schema.description="Docker Image Alpine + Java (OpenJDK)"
