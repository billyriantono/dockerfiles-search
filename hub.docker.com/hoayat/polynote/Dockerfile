FROM openjdk:8-jdk-slim

ARG POLYNOTE_VERSION="0.2.13"
ARG URL="https://github.com/polynote/polynote/releases/download/${POLYNOTE_VERSION}/polynote-dist.tar.gz"

RUN apt update && apt install -y python3 python3-pip wget
RUN pip3 install jep jedi pyspark virtualenv \
  && cd /opt \
  && wget -O polynote-dist.tar.gz $URL \
  && tar zxvf polynote-dist.tar.gz \
  && rm polynote-dist.tar.gz
ADD config.yml /opt/polynote/

EXPOSE 8000
WORKDIR /opt/polynote
CMD ["sh", "-c", "./polynote"]

LABEL maintainer="S.H.Ayat, h.ayat@sanjagh.pro"

