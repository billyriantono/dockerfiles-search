FROM alpine
ENV EDGE_REPOSITORY=http://dl-cdn.alpinelinux.org/alpine/edge/main
RUN apk update --repository $EDGE_REPOSITORY \
	&& apk add py-pip ca-certificates \
	&& apk add ffmpeg --repository $EDGE_REPOSITORY \
	&& rm -rf /var/cache/apk/*
RUN pip install youtube-dl
COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["youtube-dl","-o","/src/%(title)s-%(id)s.%(ext)s"]
