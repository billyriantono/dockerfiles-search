FROM thebijuus/docker-dl-tools:latest
MAINTAINER thebijuus@gmail.com

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /dl

ADD dlfile ./dlfile

RUN /bin/bash ./dlfile ; \
    megacopy --no-progress -u thebijuus.thebijuus@aol.com -p T5678uhbg --local /dl --remote /Root/
