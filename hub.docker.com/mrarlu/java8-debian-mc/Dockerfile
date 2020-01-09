# ----------------------------------
# Environment: Java
# ----------------------------------
FROM openjdk:8-jdk-slim

MAINTAINER VDS-mc.ru, <docker@vds-mc.ru>

RUN apt update && apt -y install lib32z1
RUN adduser -D -h /home/container container


USER container
ENV  USER=container HOME=/home/container

WORKDIR /home/container

COPY ./entrypoint.sh /entrypoint.sh

CMD ["/bin/bash", "/entrypoint.sh"]
