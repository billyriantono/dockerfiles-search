FROM debian:10-slim
LABEL maintainer "DNA"
LABEL Description="MOHAA Linux Server" Version="1.0"

RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get -y install curl tar libstdc++5:i386 wget

RUN adduser --disabled-password --home /home/mohaa mohaa

USER mohaa
ENV  USER=mohaa HOME=/home/mohaa

WORKDIR /home/mohaa

RUN wget -O mohaa-linux-server.tar.gz http://mohaa.mlt.sr/mohaa-linux-server.tar.gz
RUN tar -xzf mohaa-linux-server.tar.gz
RUN rm -f mohaa-linux-server.tar.gz

RUN chown -R mohaa:mohaa .
WORKDIR /home/mohaa

ENTRYPOINT ./mohaa_lnxded +set dedicated 1 +exec main/server.cfg
CMD []

EXPOSE 12203/udp
EXPOSE 12203/tcp