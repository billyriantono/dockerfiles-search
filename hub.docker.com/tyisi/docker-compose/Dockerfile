FROM debian:stable

WORKDIR /app

ENV DEBIAN_FRONTEND noninteractive

RUN apt update && apt upgrade -y && apt install -y wget

RUN wget -O /usr/local/bin/docker-compose "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" \
    && chmod 755 /usr/local/bin/docker-compose

ENTRYPOINT ["/usr/local/bin/docker-compose"]
