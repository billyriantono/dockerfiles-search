FROM debian:buster

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends asciidoctor curl git && \
    rm -rf /var/lib/apt/lists/*
