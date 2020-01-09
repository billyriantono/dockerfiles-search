FROM alpine:latest

RUN apk update && \
    apk add --no-cache yarn && \
    mkdir -p /opt/app

VOLUME [ "/opt/app" ]

WORKDIR /opt/app

EXPOSE 8080
