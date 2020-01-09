FROM alpine:latest

RUN apk --update --no-cache add \
    mtr \
    net-tools \
    bind-tools \
    curl \
    wget \
    jq \
    nmap \
    speedtest-cli \
    pwgen \
    openssl

COPY Dockerfile /Dockerfile
LABEL org.label-schema.docker.dockerfile="/Dockerfile" \
      org.label-schema.vcs-type="Git" \
      org.label-schema.vcs-url="https://github.com/alersrt/network-utils-alpine-docker"
