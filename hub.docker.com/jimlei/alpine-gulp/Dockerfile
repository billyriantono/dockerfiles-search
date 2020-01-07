FROM jimlei/alpine-nodejs
MAINTAINER Jim Leirvik <jim@jimleirvik.no>

RUN npm i -g gulp && \
    rm -rf /tmp/*

RUN mkdir -p /data
VOLUME /data
WORKDIR /data

ENTRYPOINT ["gulp"]
