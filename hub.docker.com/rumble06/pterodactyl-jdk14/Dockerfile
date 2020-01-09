# ----------------------------------
# Pterodactyl Core Dockerfile
# Environment: Java (glibc support)
# Minimum Panel Version: 0.6.0
# ----------------------------------
FROM        openjdk:14-alpine

LABEL       author="Michael Parker" maintainer="parker@pterodactyl.io"

RUN apk add --no-cache --update curl ca-certificates openssl git tar unzip bash sqlite fontconfig \
 && adduser -D -h /home/container container
 
USER container
ENV  USER=container HOME=/home/container

USER        container
ENV         USER=container HOME=/home/container

WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh

CMD         ["/bin/bash", "/entrypoint.sh"]
