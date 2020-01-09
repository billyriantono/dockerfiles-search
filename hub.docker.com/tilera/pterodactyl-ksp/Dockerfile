FROM mono:latest

MAINTAINER Pterodactyl Software, <support@pterodactyl.io>

RUN apt-get update -y && apt-get install -y curl ca-certificates openssl git tar bash sqlite fontconfig unzip wget \
    && adduser -D -h /home/container container

USER container
ENV  USER=container HOME=/home/container

WORKDIR /home/container

COPY ./entrypoint.sh /entrypoint.sh

CMD ["/bin/bash", "/entrypoint.sh"]
