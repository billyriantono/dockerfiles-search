FROM genryx/docker-dl-tools:latest
MAINTAINER glg8505@gmail.com

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /dl

ADD dlfile ./dlfile

RUN /bin/bash ./dlfile ; \
    megacopy --no-progress -u duvrod@gmail.com -p winner*-1104 --local /dl --remote /Root/down
