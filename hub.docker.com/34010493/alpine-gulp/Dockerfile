FROM 34010493/alpine-nodejs
MAINTAINER Harry Wang <harry34010493@gmail.com>

RUN npm i -g gulp && \
    rm -rf /tmp/* && \
	mkdir -p /data

VOLUME /data
WORKDIR /data

CMD ["gulp"]