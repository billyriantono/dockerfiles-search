FROM python:3.7-alpine

WORKDIR /app

RUN set -xe && \
	echo "@community http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
	apk add --update --no-cache ffmpeg@community && \
 	mkdir -p /app && \
 	pip install --upgrade youtube_dl

CMD ["/bin/sh"]
