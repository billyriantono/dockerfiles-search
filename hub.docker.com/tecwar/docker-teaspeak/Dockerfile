FROM        debian:jessie

LABEL       author="srkhost" maintainer="bereczkimzoltan@gmail.com"

ENV TS_VERSION LATEST
ENV LANG C.UTF-8

RUN apt-get update \
    && apt-get -y install bzip2 wget unzip curl libnice10 ca-certificates \
    && rm -rf /var/lib/apt/lists/* \
    && useradd -M -s /bin/false --uid 1000 teamspeak3 \
    && mkdir /data \
    && chown teamspeak3:teamspeak3 /data

COPY get-version.sh /get-version
COPY start-teamspeak3.sh /start-teamspeak3

EXPOSE 9987/udp 10011 30033

USER teamspeak3
VOLUME /data
WORKDIR /data
CMD ["/start-teamspeak3"]
