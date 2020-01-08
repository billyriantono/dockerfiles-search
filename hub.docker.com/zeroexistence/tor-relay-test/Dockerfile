FROM debian:buster-slim

ARG BUILD_DATE
ARG VCS_REF

LABEL maintainer="oc@co.ru" \
    com.microscaling.license="MIT" \
    org.label-schema.build-date=$BUILD_DATE \
    org.label-schema.name="Tor network client" \
    org.label-schema.url="https://www.torproject.org" \
    org.label-schema.vcs-url="https://github.com/ZeroExistence/docker-tor-simple.git" \
    org.label-schema.vcs-ref=$VCS_REF \
    org.label-schema.docker.cmd="docker run -d --rm --publish 127.0.0.1:9050:9050 --name tor zeroexistence/tor-relay-test:debian" \
    org.label-schema.schema-version="1.0"


RUN apt-get -y update && \
    apt-get --no-install-recommends -y install tor && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    mkdir -p /app && \
    chmod -R 777 /app

COPY torrc /etc/tor/torrc

EXPOSE 9001

USER 100

CMD ["/usr/bin/tor"]
