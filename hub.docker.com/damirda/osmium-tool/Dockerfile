FROM debian:stable-slim
LABEL maintainer="damir@damirda.com"

RUN apt-get update -qq && \
    apt-get install -y osmium-tool && \
    apt-get clean

WORKDIR /data
