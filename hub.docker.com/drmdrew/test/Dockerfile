FROM debian:jessie

RUN apt-get update && \
    apt-get install -y --no-install-recommends curl && \
    rm -rf /var/lib/apt/lists/*

COPY README.md /usr/src/test/README.md

RUN curl ifconfig.co
