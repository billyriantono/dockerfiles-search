FROM debian:buster

RUN apt-get update -y && \
    apt-get install -y \
    libcurl4 \
    wget \
    pcregrep \
    unzip

RUN mkdir /bedrock-server /config /worlds

WORKDIR /bedrock-server

EXPOSE 19132/udp

COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
