FROM openjdk:8u171-jre-alpine3.8

LABEL maintainer="cgiraldo@gradiant.org"
LABEL organization="gradiant.org"
ARG VERSION=3.4.0
ENV VERSION=$VERSION
ENV BIND_HOST=0.0.0.0
ENV PORT=8000
RUN mkdir /jmxproxy && \
    mkdir /jmxproxy/etc && \
    apk add --no-cache gettext && \
    wget -O /jmxproxy/jmxproxy.jar https://github.com/mk23/jmxproxy/releases/download/jmxproxy.$VERSION/jmxproxy-$VERSION.jar
COPY jmxproxy.yaml.tpl /jmxproxy/etc/jmxproxy.yaml.tpl
COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT /entrypoint.sh
