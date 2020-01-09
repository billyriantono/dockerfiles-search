
# ----------------------------------
# Pterodactyl Java 11 Core FIle
# Environment: Java 
# Minimum Panel Version: 0.6.0
# ----------------------------------
FROM        openjdk:11-jre-slim

LABEL       original_author="Michael Parker" maintainer="parker@pterodactyl.io"
LABEL       author="Lukas Babohn" maintainer="lukas@babohn.de"

RUN apt-get update -y \
 && apt-get install -y curl ca-certificates openssl git tar sqlite fontconfig tzdata iproute2 \
 && useradd -d /home/container -m container
 
USER container
ENV  USER=container HOME=/home/container

USER        container
ENV         USER=container HOME=/home/container

WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh

CMD ["/bin/bash", "/entrypoint.sh"]
