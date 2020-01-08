FROM busybox as builder

ADD https://minecraft.azureedge.net/bin-linux/bedrock-server-1.12.0.28.zip /server.zip

RUN mkdir /server
RUN unzip /server.zip -d /server

FROM ubuntu:bionic

MAINTAINER Mush Mo <mush@pandorica.io>

ENV LD_LIBRARY_PATH /data

RUN apt-get update && apt-get install -y \
    curl \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /data

ADD ./entrypoint /opt/entrypoint

EXPOSE 19132/udp

COPY --from=builder /server /opt/mc

ENTRYPOINT ["/opt/entrypoint"]
